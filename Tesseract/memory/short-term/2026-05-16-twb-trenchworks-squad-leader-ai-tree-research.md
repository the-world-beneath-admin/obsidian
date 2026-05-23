# TWB Trenchworks Squad-Leader AI Tree Research

Date: 2026-05-16

Scope: standalone TWB-tagged game, specifically the Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

Worker boundary: research/design report only. No source code changed. No permanent wiki, index, hot, or log files changed.

## Sources Researched

- [A Survey of Real-Time Strategy Game AI Research and Competition in StarCraft](https://davechurchill.ca/publications/pdf/starcraft_survey.pdf) - useful for RTS constraints, fog-of-war, real-time branching factor, bot architecture, blackboard/shared data, squad/combat modules, hierarchical abstraction, and divide-and-conquer systems.
- [Adversarial Hierarchical-Task Network Planning for Complex Real-Time Games](https://www.ijcai.org/Proceedings/15/Papers/236.pdf) - useful for why RTS games need hierarchical decomposition under time pressure instead of exhaustive planning.
- [Kiting in RTS Games Using Influence Maps](https://ojs.aaai.org/index.php/AIIDE/article/view/12544) - useful for tactical multi-unit movement where influence maps support attack/flee behavior.
- [Co-evolving Real-Time Strategy Game Players](https://www.cse.unr.edu/~sushil/pubs/newestPapers/2011/tciaig/coevolveRTS/coevolveRTS.html) - useful for influence-map trees as spatial objective selectors in RTS play.
- [Game AI Pro - The Behavior Tree Starter Kit](https://www.gameaipro.com/GameAIPro/GameAIPro_Chapter06_The_Behavior_Tree_Starter_Kit.pdf) - useful for BT tick model, selectors/sequences/actions/conditions, blackboard/action dependencies, and throttled update rates.
- [Game AI Pro - Building Utility Decisions into Your Existing Behavior Tree](https://www.gameaipro.com/GameAIPro/GameAIPro_Chapter10_Building_Utility_Decisions_into_Your_Existing_Behavior_Tree.pdf) - useful for combining BT structure with utility scoring when priorities are contextual rather than fixed.
- [Behavior Trees: Breaking the Cycle of Misuse](https://takinginitiative.net/2020/01/07/behavior-trees-breaking-the-cycle-of-misuse/) - useful warning against monolithic BTs and against confusing decision-making with actuation.
- [Game AI Pro - Modular Tactical Influence Maps](https://www.gameaipro.com/GameAIPro2/GameAIPro2_Chapter30_Modular_Tactical_Influence_Maps.pdf) - useful for layered tactical maps: friendly/enemy pressure, danger, terrain, fronts, flanks, and spatial desirability.
- [Company of Heroes 2 manual - Cover](https://www.feralinteractive.com/en/manuals/companyofheroes2/latest/steam/#cover) - useful strategy/squad framing for heavy/light/negative/directional cover and suppression-relevant squad vulnerability.
- [Game AI Pro - Phenomenal AI Level-of-Detail Control with the LOD Trader](https://www.gameaipro.com/GameAIPro/GameAIPro_Chapter14_Phenomenal_AI_Level-of-Detail_Control_with_the_LOD_Trader.pdf) - useful for AI LOD based on importance/observability/budget, not only distance.
- [Simulation Level of Detail for Multiagent Control](https://publications.ri.cmu.edu/simulation-level-of-detail-for-multiagent-control) - useful for simplified simulation models in large multi-agent navigation/control.
- Current prototype files inspected: `WarTeamTypes.cs`, `WarTeamEntities.cs`, `WarTeamSlice.cs`, `WarIntegrationFacade.cs`, and `WarTeamScenariosDiagnostics.cs`.

## How Strategy-Game AI Commonly Structures These Decisions

Strategy-game AI usually separates the problem into layers rather than asking each unit to be a tiny general. Common layers are:

- Strategic layer: doctrine, economy, production, objectives, broad attack/defend timing.
- Operational layer: squads/armies/fronts, reinforcement choices, lane assignment, supply routing, scouting, expansion.
- Tactical layer: local movement, cover choice, target pressure, retreat, suppression, cohesion, formation slots.
- Actuation layer: move, shoot, dig, heal, carry, reload/resupply, enter trench, hold posture.

The StarCraft bot survey is especially relevant because it describes real RTS agents as mixtures of hierarchical abstraction and divide-and-conquer modules. Combat often gets its own hierarchy, while economy, scouting, construction, and production are separate modules. Some bots coordinate through a shared blackboard; others use an arbitrator to prevent contradictory orders. This maps well to Trenchworks: production/logistics should not live inside squad AI, but squad AI must consume logistics state through blackboard variables.

Behavior trees are common because they are readable and reactive, but the research is quite firm on a trap: giant trees become brittle. A behavior tree is better as a structured executor and guard system, while the hard tactical choice between "advance", "hold", "dig in", "retreat", and "resupply" is better done by scoring candidates. Utility AI is the practical addition: compute contextual scores from danger, cover, contact certainty, supply, morale, cohesion, role, doctrine, and trench value.

HTN planning is useful at higher levels where tasks naturally decompose: "secure lane" -> "scout forward" -> "establish contact" -> "choose covered position" -> "dig firing trench" -> "connect communication trench" -> "hold/resupply". For the current prototype, a full HTN planner is too much ceremony. Use HTN-like task decomposition in data and code comments, not a full planner yet. A proper HTN becomes attractive later if command units assemble multi-squad missions with prerequisites and fallback plans.

Influence maps are the most important strategy-game idea for this prototype. They let squads reason spatially without scanning the whole world like omniscient chess pieces. Trenchworks already has the beginnings of this in `SampleInfluence`: local candidate cells, cover, contact, danger, scout value, supply reach, and friendly trench value. This should become the squad leader's tactical sense organ.

Perception should be blackboard-driven and imperfect. Strategy games commonly operate under fog-of-war; the AI should distinguish visible enemies, suspected contacts, sound events, last-known positions, and communicated contacts. This is vital for avoiding FPS-only "I saw the player, chase the player" framing.

Formation and squad cohesion are usually handled by a leader/anchor plus slots, not by every unit making strategic choices. Individual roles can affect local action, but the leader chooses squad intent. Members then execute role-specific actuation inside that intent.

LOD and throttling matter once the war grows. The prototype should not tick every squad at full tactical detail forever. Nearby/in-contact/visible/important squads get full decisions. Rear-area or offscreen squads can use lower-frequency decisions and coarser movement/combat summaries.

## Recommendation

Use a general squad-leader decision model with data-driven specialization overlays. Do not build a unique behavior tree per squad leader for this prototype.

The practical structure:

1. Shared squad leader decision kernel.
2. Shared blackboard/perception refresh.
3. Shared influence/candidate generator.
4. Shared behavior-tree outline for gating and execution.
5. Utility scoring layer for choosing the squad intent and target.
6. Per-squad template overlays for role weights, thresholds, preferred tasks, and forbidden tasks.
7. Per-member role actuation under the selected squad intent.

This gives the prototype flexibility without turning AI design into a hedge maze. A scout patrol, assault section, fortify engineer crew, and supply team can all use the same leader brain while feeling different through weighted preferences:

- scout: high caution, high unknown-cell value, low direct-assault appetite.
- assault: high contact pressure, higher ammo dependency, better suppression tolerance.
- engineer/sapper: high held-contact/trench-value preference, high construction dependency.
- medic/quartermaster: high casualty/supply/morale response, low front-edge appetite.

Unique trees should be reserved for genuinely different command species later, such as artillery observer, tunnel raider, armored column, or enemy boss commander. Even then, prefer subtree overlays and different scoring profiles before new whole trees.

## Proposed Squad-Leader Decision Model

Use a "tree-shaped policy with utility selectors" rather than a pure static behavior tree.

Text outline:

```text
SquadLeaderRoot
  RefreshBlackboard
    Read own team state: role mix, leader alive, morale, cohesion, casualties, ammo, food, medical, construction
    Read local perception: visible contacts, suspected contacts, sound events, last-known enemy positions
    Read terrain: cover, trench value, slow terrain, negative cover, supply reach, route risk
    Read strategic context: doctrine, lane, mission order, friendly nearby squads, current front pressure

  EmergencySelector
    If leader dead or alive count too low -> RegroupOrWithdraw
    If cohesion broken -> RegroupOnLeader
    If food/ammo critically low and not trapped -> RequestResupplyOrFallBack
    If pinned/suppressed and no cover/trench -> CrawlToNearestCoverOrGoProne
    If wounded cluster and medic present -> TreatUnderCover

  ContactSelector
    If confirmed contact:
      Evaluate combat edge
      If danger high and edge poor -> HoldInCover / Suppress / RetreatByBounds
      If cover nearby and not in cover -> MoveToCoverFacingThreat
      If edge neutral -> HoldAndCallNearbyUnits
      If edge positive and position not fortified -> DigInOrImproveCover
      If edge positive and trench held -> HoldTrench, connect trench, or request supply
      If assault profile and edge strongly positive -> BoundForwardToNextCover

    If suspected contact or hearing event:
      If scout/assault and supply ok -> InvestigateByCoveredRoute
      If engineer/supply -> HoldOrMoveToFriendlyTrench
      Broadcast/merge suspected contact on faction blackboard

  NoContactSelector
    If mission is Scout -> AdvanceToReconCandidate using forward-biased lateral sampling
    If mission is Assault -> AdvanceCoverToCover, not straight-line charge
    If mission is Fortify -> MoveToHeldOrHighValuePosition, then DigIn
    If mission is ConnectTrenches -> Work communication trench toward base/supply route
    If mission is Supply -> Move to most needy friendly squad or depot
    If mission is Hold -> Occupy best cover/trench and preserve readiness

  UtilityCandidateScoring
    Generate local candidates in an advance cone plus lateral/cover cells
    Score each candidate:
      + mission value
      + cover value
      + friendly trench value
      + supply reach
      + fog/scout value
      + friendly support proximity
      - danger/threat
      - negative cover
      - overextension
      - cohesion stretch
      - low supply penalty
      - repeated straight-line advance penalty

  CommitIntent
    Set TeamDecisionKind and target
    Set squad posture
    Emit reason string for diagnostics
    Optionally emit sound/contact/supply request event

  RoleActuation
    Leader moves anchor
    Riflemen face/suppress/guard
    Scouts probe and report
    Sappers dig or breach
    Engineers fortify/connect
    Medics treat if safe enough
    Quartermasters/porters deliver supplies
```

Key design point: the tree decides "what class of problem are we solving?" Utility scoring decides "which specific action/position is best right now?" Actuation then moves individual members. This keeps behavior readable and tunable.

## Blackboard and Perception Variables Needed

Team identity and capability:

- `TeamId`, `Faction`, `TemplateId`, `TeamKind`, `Order`, `EntryLane`
- `LeaderId`, `LeaderAlive`, `Anchor`, `Target`
- `AliveCount`, `Casualties`, `RoleCounts`
- `Morale`, `Cohesion`, `Suppression`, `Fatigue`
- `Ammo`, `Food`, `Medical`, `Construction`
- `SupplyCritical`, `AmmoLow`, `ConstructionLow`, `MedicalLow`
- `Caution`, `Aggression`, `Engineering`, `MedicPriority`, `SupplyPriority`

Perception and fog:

- `VisibleEnemyContacts`
- `SuspectedContacts`
- `LastKnownEnemyPositions`
- `ContactConfidence`
- `ContactHeat`
- `HeardEvents`: gunfire, explosion, digging, movement, distress call
- `KnownFriendlySquads`
- `KnownFriendlyTrenches`
- `KnownSupplyRoutes`
- `ExploredCells` / `KnownCells` / `UnknownCells`
- `CanSeeCell` and `LineOfSightBlocked`

Spatial/tactical maps:

- `CoverKind` with future directional facing
- `ThreatMap` / `Danger`
- `FriendlyInfluence`
- `EnemyInfluence` from known/suspected enemies only
- `TrenchValue`
- `FortificationValue`
- `SupplyReach`
- `MovementCost`
- `RouteRisk`
- `NoMansLandPressure`

Decision memory:

- `CurrentIntent`
- `IntentStartedTick`
- `LastDecisionKind`
- `LastTarget`
- `LastReason`
- `RecentTargets` to discourage jitter
- `RecentAdvanceVector` to discourage straight-line charging
- `HoldUntilTick`
- `LastResupplyRequestTick`
- `LastHeardResponseTick`
- `CombatEdgeEstimate`

Shared faction blackboard:

- contact reports with time/confidence/source squad
- sound-event heat
- supply requests
- trench network plans
- front-line/held-line summaries
- squad assignments and reserved targets to prevent pileups

## Per-Squad Specialization Examples

Scout patrol:

- High weight for unknown cells, suspected contact investigation, concealment, and survival.
- Lower weight for confirmed attack.
- On confirmed contact with high danger, hold in cover and report rather than charge.
- Should move in a forward-biased zig-zag or cover chain, not a direct line.

Assault section:

- High weight for confirmed contact, suppressive posture, and advancing to the next covered firing position.
- Requires ammo threshold before attack.
- If danger exceeds combat edge, hold or request support instead of pushing.
- Sapper member can increase breach/dig utility but should not make the whole squad behave like engineers.

Fortify engineer crew:

- High weight for held or consolidated contact cells, friendly trench extension, and communication trench back to base.
- Requires construction supply.
- Should avoid leading blind advances unless ordered and escorted.
- Once a combat edge appears, dig in first, then hold/connect rather than immediately pushing.

Supply team:

- High weight for low-stock friendly squads, supply-route safety, and friendly trench value.
- Avoid confirmed contact unless forced.
- Emits resupply completion and can improve morale/cohesion of nearby squads.
- Should use lower LOD safely when rear-area and not near contact.

Medic/quartermaster mixed team:

- High weight for casualty clusters, morale recovery, and stabilizing pinned squads.
- Moves only if route risk is acceptable or friendly cover/trench path exists.
- Can convert "retreat" into "regroup at aid post/supply node" once those systems exist.

Future specialist examples:

- Sapper raiders: high trench-breach/tunnel/sabotage utility, high danger tolerance, low hold preference.
- Machine-gun team: high setup/hold/suppress utility, low moving assault utility, directional firing arc.
- Artillery observer: high line-of-sight/known-contact reporting utility, low close combat utility.
- Tunnel crew: underground route scoring, sound-risk and collapse-risk blackboard variables.

## Concrete Implementation Steps for the Current Unity/C# Prototype

No code was changed during this pass. These are recommended next implementation steps.

1. Preserve the current `WarTeamSlice` foundation, but split the large `ChooseDecision` conceptually into separate pure C# pieces:
   - blackboard refresh
   - candidate generation
   - utility scoring
   - intent selection
   - actuation/apply decision

2. Extend `InfluenceSample` into a richer candidate model rather than sampling only a 3x3 forward patch. Candidate generation should include:
   - forward cone
   - lateral offsets
   - nearest cover cells
   - nearest friendly trench cells
   - suspected contact cells
   - fallback/regroup cells
   - supply-route cells

3. Add a straight-line advance penalty. Track recent targets or recent advance vectors per team. Reward mild lateral movement and cover-to-cover stepping. This alone will make scouting feel much less like a parade into a meat grinder.

4. Add `CombatEdgeEstimate` as a computed value:
   - friendly strength near target
   - known/suspected enemy strength
   - cover/trench advantage
   - ammo/readiness
   - morale/cohesion
   - medic/engineer support
   - supply reach
   - danger/contact heat

5. Change "dig in" from only contact-state gating to a utility outcome:
   - contact held or combat edge positive
   - construction available
   - position has cover/trench potential
   - supply route not hopeless
   - overextension below threshold

6. Add "hold trench" as a first-class decision distinct from `DigIn`.
   - Current decisions include `Hold`, `DigIn`, and `ConnectTrenches`; this is enough for now, but diagnostics should explicitly state "holding trench" when trench value is high.
   - Do not let every positive combat edge become an attack. The trench fantasy requires holding won ground.

7. Add hearing/sound events before complex vision:
   - confirmed contact and attacks emit sound events with radius and heat.
   - nearby friendly squads convert sound into suspected contact.
   - scouts/assault may converge; engineers/supply prefer hold or support route.
   - throttle response so the whole map does not blob into one brawl.

8. Add fog-of-war honesty:
   - decisions should use visible and reported/suspected contact, not hidden true enemy state.
   - enemy AI can use its own faction blackboard.
   - debugging views may show truth, but decision reasons should disclose whether target was visible, suspected, heard, or reported.

9. Keep role execution subordinate to squad intent:
   - leader anchor chooses target.
   - members fill formation slots.
   - riflemen suppress/guard.
   - scouts improve sight/contact confidence.
   - sappers/engineers contribute work to trench/breach tasks.
   - medics reduce casualty/morale penalties only when posture/risk allows.

10. Expand deterministic smoke scenarios in `WarTeamScenariosDiagnostics.cs`:
   - scout avoids straight-line charge and selects lateral cover
   - assault holds when danger exceeds edge
   - engineers dig in after edge appears
   - squads hold trench rather than immediately pushing
   - supply team serves low-stock squad
   - nearby squad responds to hearing event
   - fogged enemy is not targeted as confirmed
   - low cohesion triggers regroup

11. Add LOD tiers only after the behavior is legible:
   - LOD 0: visible/in-contact squads, full candidate scoring every tactical tick.
   - LOD 1: nearby front squads, full scoring every few ticks with cached candidates.
   - LOD 2: rear/supply/offscreen squads, coarse intent update and simple movement.
   - LOD 3: abstracted front contribution only for far-away, non-observed squads.

## Risks and Simplifications

- Risk: a giant behavior tree will become unmaintainable. Keep the tree shallow and put contextual choice into utility scoring.
- Risk: unique leader trees will duplicate logic and make future role additions expensive. Use profiles/overlays first.
- Risk: influence scoring can become inscrutable. Every decision should emit a short reason string and key score components.
- Risk: cover seeking can cause jitter. Use commitment windows, target hysteresis, and recent-target penalties.
- Risk: hearing response can create unrealistic blobs. Add response cooldowns, squad caps per event, and role-based refusal.
- Risk: fog-of-war bugs can make AI feel psychic. Keep truth maps separate from faction knowledge maps.
- Risk: engineers may over-dig and stall the war. Gate digging by combat edge, construction supply, and strategic value.
- Risk: supply awareness can paralyze squads. Let low supply bias actions before it hard-blocks them; reserve hard blocks for critical thresholds.
- Simplification: do not implement full HTN planning yet. Use HTN-like decomposition in the shared leader model and reserve real HTN for later multi-squad command operations.
- Simplification: directional cover can wait. Start with cover value and later add facing/flanking once movement and trench holding feel good.
- Simplification: suppression can start as morale/cohesion/danger posture effects before modeling fire lanes and weapons in detail.

## Bottom Line

For Trenchworks, the right prototype architecture is a shared squad-leader decision model with specialization overlays. The squad leader should own intent, the blackboard should own imperfect knowledge, influence maps should nominate positions, utility should choose between tactical options, and role-specific members should execute inside the squad intent.

This supports the requested behaviors: squad movement under a leader, forward-biased but non-suicidal scouting, cover-to-cover advance, contact posture changes, digging in when an edge appears, holding trenches, hearing-based convergence, supply-aware restraint, fog-of-war limits, engineer/sapper/medic/rifle roles, and future specialist teams.
