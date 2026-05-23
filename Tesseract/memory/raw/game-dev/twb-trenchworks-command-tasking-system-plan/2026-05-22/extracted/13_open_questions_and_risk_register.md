# 13 — Open Questions and Risk Register

## Purpose

This file lists design questions Bob should answer before coding deep behavior, plus implementation risks and mitigations.

The most important warning: the idea is broad. The system should be built in gates, with debug visibility early.

---

## Top design decisions Bob should approve before coding

### 1. Where should mission state live?

| Option | Pros | Cons |
|---|---|---|
| Add mission fields to `WarTeam` | Easy lookup, visible in entity state | Save migration risk; entity gets larger |
| Command-side mission map keyed by team ID | Less invasive, easier rollback | Need careful cleanup when teams die/despawn |
| Hybrid: `WarTeam.ActiveMissionId` + command map | Good balance | Requires ID discipline |

Recommended: hybrid.

### 2. Should Player General be automatic only, or doctrine-driven?

| Option | Meaning |
|---|---|
| Automatic Balanced only | Simpler Phase 1. |
| Doctrine dropdown/toggle | Bob can steer mission choices. |
| Per-lane doctrine | More control, more UI/scope. |

Recommended: start with automatic `Balanced`, but design data contracts for doctrine.

### 3. How much should missions influence existing `ChooseDecisionCore(...)` at first?

| Option | Meaning |
|---|---|
| Label only | No behavior change, safest. |
| Soft bias | Mission hints influence existing decisions. |
| Hard override | Mission picks decision directly. |

Recommended: label only Gate 1-2, soft bias Gate 4. Avoid hard override until tests are strong.

### 4. What enemy difficulty should be the default target?

| Tier | Use |
|---|---|
| Recruit | Tutorial/easy pressure. |
| Regular | Default balanced skirmish. |
| Veteran | Hard pressure. |
| Brutal | Challenge/testing only. |

Recommended: tune around `Regular`, then scale down/up.

### 5. Which future squad family comes first after the four live templates?

| Family | Why |
|---|---|
| MG | Tests hardpoint occupation and ammo support. |
| Aid | Tests casualty support chain. |
| Mortar | Tests support requests and spotting. |
| Command/signals | Tests relay and support coordination. |

Recommended: MG first if hardpoint sockets are ready; Aid first if casualty systems are more mature.

---

## Additional open questions

### Spawn/lane data

- What exact type identifies a selected lane/zone today?
- Does `SpawnWarTeamFromInterface(...)` return a `WarTeam`/ID, or does Codex need to find it after spawn?
- Are player and enemy spawn zones symmetrical or separate data?
- Are enemy spawn zones already represented in `WarFrontAssignmentPlanner`?

### Save/load

- Is there an existing save system?
- Should command state be saved immediately or debug-only in Phase 1?
- How are team IDs persisted today?

### Tick rate and timing

- What is the simulation tick rate?
- What tick durations feel right for retask cooldowns?
- How often should Enemy General evaluate spawn eligibility?

### Hardpoints and sockets

- Are hardpoint sockets explicit IDs today?
- Can hardpoints define multiple crew/work slots?
- Is rifle/firing bay occupation already represented?
- Is MG point currently buildable, planned, or only cataloged?

### Support requests

- Where are support requests currently stored?
- Are requests per team, per lane, or global?
- Can more than one squad claim a support request today?
- How does a support request close?

### Visibility

- What is the current player visibility/minimap model?
- Does enemy use same visibility model?
- Are `VisibleFrontBlueprintPieces` player-only or faction-aware?

### Member movement

- Are `WarSubUnit` members physically independent enough for tasks?
- Or should member tasks remain abstract until movement supports them?
- How are member positions and sockets updated today?

### Existing docs

Before coding, Codex should read the listed docs and check for conflicts:

```text
trenchworks-unit-tactics-implementation-fix-plan.md
trenchworks-unit-and-squad-expansion-design.md
trenchworks-phase-1-combat-expansion-master-plan-v1.md
phase1-front-establishment-gate-00-master-plan.md
phase1-squad-unit-local-wiki.md
gpt-pro-unit-tactics-doctrine-output-intake-2026-05-17.md
gpt-pro-unit-tactics-doctrine-research-prompt.md
```

---

## Risk register

### Risk: overcomplexity

Problem: the full plan covers generals, missions, leader brains, member tasks, reactions, claims, enemy difficulty, and debug UI. Implementing it all at once will likely fail.

Mitigation:

- Gate the work.
- Gate 1 must be shadow-only.
- Add one behavior layer at a time.
- Keep the four live templates as initial scope.
- Keep future 50 templates on the shelf.

Severity: High.

### Risk: hidden state hard to debug

Problem: missions, claims, support requests, and enemy budgets can make squads look wrong if Bob cannot inspect reasons.

Mitigation: add command event log early, add selected-squad mission reason before active behavior, add claim/support overlays before deep member tasks, and require readable reason strings.

Severity: High.

### Risk: too much autonomous control reduces player agency

Problem: if the Player General overrides Bob’s choices too strongly, it can feel like the game plays itself.

Mitigation: player chooses spawn type/lane/doctrine; General assigns bounded mission based on those choices; UI shows reason; add doctrine controls later; avoid auto-spawning player squads.

Severity: Medium-high.

### Risk: unfair enemy information

Problem: Enemy General may feel like it cheats if it instantly counters hidden player actions.

Mitigation: use difficulty-specific info access, response delays, information noise, budget/caps, debug-only internal enemy info, and no hidden info leaks in normal UI.

Severity: High.

### Risk: performance cost

Problem: scoring missions for many squads, claims, member tasks, and debug logging can grow expensive.

Mitigation: score only on spawn, retask trigger, or periodic interval; use snapshots; use small catalogs; use ring buffers; avoid per-member deep logic until needed; avoid allocations in hot tick loops.

Severity: Medium.

### Risk: save-state migration

Problem: adding mission/task/claim state to `WarTeam` may break saves or future save design.

Mitigation: use schema version, start with command-side sidecar map, save only stable state, avoid saving debug candidate lists, and add default migration where no mission becomes fallback on load.

Severity: Medium.

### Risk: implementation scope creep

Problem: the 50 planned templates and many hardpoint families can tempt too much implementation.

Mitigation: Phase 1 only live four templates; future MG/Mortar/Aid/Command as later gates; add one hardpoint family at a time; acceptance criteria per gate.

Severity: High.

### Risk: conflict with existing front assignment logic

Problem: a new command layer could duplicate or fight `WarFrontAssignmentPlanner`.

Mitigation: use planner as target provider, do not create a separate front model, let claims constrain planner outputs rather than replacing it, and keep existing `WarTeamSlice` behavior until mission hints are proven.

Severity: High.

### Risk: `WarTeamSlice.ChooseDecisionCore(...)` becomes more monolithic

Problem: adding missions, difficulty, claims, leader states, and member tasks directly into `ChooseDecisionCore(...)` will make it unmaintainable.

Mitigation: add `SquadMissionController`, add small helper methods, keep mission scoring outside slice, let slice consume decision hints, and move leader/member logic to separate classes.

Severity: High.

### Risk: retask thrashing

Problem: squads can repeatedly switch missions due to small score changes.

Mitigation: retask cooldowns, score margin threshold, emergency-only immediate retask, stable tie-breakers, and event log retask rate counter.

Severity: Medium-high.

### Risk: claim deadlocks

Problem: a team can hold a claim while unable to progress, blocking everyone else.

Mitigation: TTL expiration, progress renewal required, release on no path, debug clear-claims tool, and event log for claim expiration.

Severity: Medium.

### Risk: member tasks conflict with physical simulation

Problem: if members do not have enough movement/socket support, active tasks may fight existing movement/combat logic.

Mitigation: shadow mode first, activate tiny task subset, use posture/task hints before direct movement, and keep squad-level decisions authoritative until member tasks are proven.

Severity: High.

### Risk: support teams die trying to answer impossible requests

Problem: supply/aid teams may chase requests through unsafe contact.

Mitigation: safe path checks, support claim expires if no route, fallback to reserve/regroup, support request remains open for later, and route safety included in score.

Severity: Medium.

### Risk: future exotic roles create unbounded behavior

Problem: special roles like `PressureProjector`, `AetherLampScout`, or `BoundShellCantor` can blow up scope.

Mitigation: map them to existing action families first, add special behavior only after base roles are stable, and keep every special action in the same mission/task/reaction catalog system.

Severity: Medium.

---

## Recommended next decision before coding

Approve this Phase 1 stance:

```text
Gate 1 will add shadow command contracts, command event log, and WarCommandDirector stub only.
Gate 2 will assign missions to player-spawned squads but will not force member behavior.
The first active behavior change will be mission-level decision bias, not full member AI.
Enemy General replacement waits until mission assignment and debug UI are visible.
```

This keeps the project safe, debuggable, and testable while still moving toward the full command/tasking system.

---

## Final pushback

The concept is strong, but the dangerous part is scope. The correct first win is not “smart squads.” The correct first win is:

```text
Every squad has one visible mission, one readable reason, and no gameplay regression.
```

Once Bob can see that, deeper squad leader and member behavior can be added without guessing.
