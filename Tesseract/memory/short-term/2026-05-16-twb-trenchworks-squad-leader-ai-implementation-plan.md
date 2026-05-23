# TWB Trenchworks Squad-Leader AI Implementation Plan

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity prototype.

## Summary

Use a shared squad-leader decision model with data-driven specialization overlays.

Do not build a unique behavior tree for every squad leader. That would duplicate logic and make the AI harder to tune. The better Trenchworks pattern is:

1. Shared squad blackboard.
2. Shared leader decision tree.
3. Utility scoring inside selected tree branches.
4. Squad-type profiles that change weights and thresholds.
5. Role-specific member actuation under the leader's chosen intent.

This fits the current code because `WarTeamSlice.ChooseDecision` already has early pieces of this: team kind, order, supply, contact state, danger, scout value, trench value, and decision reasons.

## Current Code Shape

Relevant files:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamTypes.cs`

Current issue:

- The visible wave-drill layer still uses an imperative `TickUnit` priority chain.
- The newer `WarTeamSlice` already has better squad/team semantics but is not yet the single canonical frontline behavior model.
- There is a risk of maintaining two AI systems unless future work either shares the same decision model or slowly retires the legacy unit loop.

## Proposed Decision Tree

```text
SquadLeaderRoot
  RefreshBlackboard
    Team health, cohesion, morale, ammo, food, construction, casualties
    Visible contacts, suspected contacts, heard contacts, last known enemy
    Cover, trench value, movement cost, route risk, supply reach
    Mission order, doctrine, lane, nearby friendly squads

  EmergencySelector
    Leader dead or team too small -> Regroup / Withdraw
    Cohesion broken -> RegroupOnLeader
    Critical supply -> RequestSupply / FallBackToSupply
    Pinned and exposed -> CrawlToCover / GoProne

  ContactSelector
    Confirmed contact:
      Score combat edge
      Poor edge + high danger -> HoldInCover / RetreatByBounds
      Not in cover -> MoveToCoverFacingThreat
      Neutral edge -> HoldAndCallSupport
      Positive edge + not fortified -> DigIn
      Positive edge + trench exists -> HoldTrench / ConnectTrench
      Strong edge + assault profile -> BoundForwardToNextCover

    Suspected/heard contact:
      Scout/assault -> InvestigateByCoveredRoute
      Engineer/supply -> Hold / Support from trench
      Broadcast contact to faction blackboard

  NoContactSelector
    Scout -> Forward-biased covered recon
    Assault -> Cover-to-cover advance
    Fortify -> Move to high-value held ground, then dig
    Supply -> Move to most needy friendly squad or depot
    Hold -> Occupy cover/trench and preserve readiness

  UtilityCandidateScoring
    Score candidate cells by mission value, cover, trench, support, scout value, supply reach
    Penalize danger, overextension, low supply, cohesion stretch, negative cover, repeated straight-line motion

  CommitIntent
    Set decision kind, target, posture, and reason string

  RoleActuation
    Leader moves anchor
    Riflemen suppress/guard
    Scouts improve contact confidence
    Sappers/engineers dig or breach
    Medics stabilize morale/health
    Porters deliver supplies
```

## First Coding Pass

Keep the first implementation small and legible.

1. Add a richer `SquadDecisionBlackboard` or extend `InfluenceSample`.
   - Include contact confidence, combat edge, nearest cover, friendly support count, supply critical flags, and recent direction/target.

2. Split `WarTeamSlice.ChooseDecision` into smaller private methods.
   - `BuildBlackboard(team)`
   - `GenerateCandidateCells(team, blackboard)`
   - `ScoreCandidate(team, candidate, blackboard)`
   - `ChooseIntent(team, blackboard, bestCandidate)`
   - `ApplyDecision(team, decision)`

3. Add squad profile weights to `WarTeamTemplate`.
   - Scout: high unknown/scout value, high caution, low attack.
   - Assault: high confirmed-contact pressure, ammo threshold, higher risk tolerance.
   - FortifyEngineer: high held-contact/trench/construction value.
   - Supply: high needy-friendly value, high route safety, low contact appetite.

4. Add straight-line prevention.
   - Track recent target or recent advance vector per team.
   - Penalize repeatedly choosing the same direct-forward vector.
   - Reward mild lateral movement when advancing.

5. Add combat edge.
   - Friendly strength, enemy/contact heat, cover, trench, ammo, morale, support, supply reach.
   - Positive edge should bias toward digging/holding before attacking.

6. Add `HoldTrench` as a diagnostic reason first.
   - Do not add a new enum unless needed.
   - Use existing `TeamDecisionKind.Hold` with reason `holding trench: ...`.

7. Add hearing response as suspected contact.
   - Contact emits sound heat.
   - Nearby squads can investigate or support depending on profile.
   - Add cooldown/cap so the whole map does not collapse into one brawl.

8. Add tests/smoke diagnostics in the war team diagnostics area.
   - Scout avoids straight-line route.
   - Assault holds when danger beats edge.
   - Engineer digs after edge appears.
   - Squad holds trench instead of immediately advancing.
   - Supply team serves low-stock team.
   - Fogged enemy is not treated as confirmed.

## Implementation Caution

The next pass should start inside `WarTeamSlice` rather than the legacy `WarWorld.TickUnit` loop. Once the team-layer behavior is better, the visible wave-drill can either mirror those decisions or migrate toward rendering/simulating teams as the canonical battlefield objects.

## Research Basis

Primary worker report:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-squad-leader-ai-tree-research.md`

Additional notes:

- Behavior trees are useful for readable structure, but giant trees become brittle.
- Utility scoring is better for contextual choices such as advance, hold, dig, retreat, or resupply.
- Influence maps/candidate scoring are the best match for a large RTS-style battlefield under fog of war.
- Blackboard variables should store squad-level perception and decision memory, not every tiny one-off calculation.

## Risks

- Too much AI complexity can make behavior harder to diagnose.
- Hearing response can create unrealistic blobs unless capped.
- Cover scoring can cause jitter without commitment windows or recent-target penalties.
- Fog-of-war must not let AI target hidden true-state enemies as confirmed contacts.
- Maintaining both `WarWorld` and `WarTeamSlice` behavior paths will become expensive if they diverge further.

## Recommended Next Step

Implement the first coding pass in `WarTeamSlice` with debug-friendly decision reasons, then wire the visible wave drill closer to the team-layer decisions once the behavior reads correctly.
