# TWB Trenchworks Command Tasking System Plan - Verbatim Transcript

Source ZIP: C:\Users\yrred\Downloads\twb-trenchworks-command-tasking-system-plan.zip
Original ZIP SHA256: F8E7B8A65F0867EB6E1541688D7A005C969DD6AE06EA733FBB9814B70116CE8A
Note: File contents below are transcribed verbatim between BEGIN/END markers. The extracted files in the sibling extracted folder are byte-for-byte copies from the ZIP.

<!-- BEGIN FILE: 00_readme_and_package_manifest.md -->
# TWB Trenchworks Command / Tasking System Plan

## Package purpose

This package is an implementation-planning set for a multi-tier command and tasking system in **TWB Trenchworks**, a standalone Unity 2D factory/logistics and automated trench-war simulation under The World Beneath umbrella.

The goal is to give a Codex worker a safe, staged, deterministic plan for moving from the current local `WarTeamSlice.ChooseDecisionCore(...)`-centered behavior toward a bounded command stack:

```text
General Strategy / Spawn Policy
  -> Squad Mission Assignment
    -> Squad Leader Task State
      -> Member Role Task
        -> Member Action / Reaction Tree
```

This is not production code. It is an architecture and implementation plan. Real-world tactics are intentionally abstracted into game simulation behavior such as lane pressure, contact heat, hardpoint sockets, support requests, and front depth.

## Source and scope note

This plan is grounded in the provided planning prompt and its listed current-code vocabulary. The actual Unity project files were not inspected in this package pass. When the prompt lists concrete classes, methods, enums, and current flow, those are treated as confirmed project facts for planning purposes. Any proposed new type, enum, state machine, or gate is marked as a recommendation.

## Files included

| File | Purpose |
|---|---|
| `00_readme_and_package_manifest.md` | Package overview, reading order, executive summary, roadmap. |
| `01_current_system_analysis.md` | Current spawn/team/front/contact/enemy-response analysis and preservation guidance. |
| `02_command_hierarchy_architecture.md` | Proposed command hierarchy, ownership boundaries, sequence diagrams, lifecycle diagrams. |
| `03_data_contracts_and_state_model.md` | Proposed data contracts, enums, records, serialization and determinism notes. |
| `04_player_general_mission_assignment.md` | Player General mission-scoring and retasking plan by squad type. |
| `05_enemy_general_spawn_tasking_difficulty.md` | Enemy General virtual budget, spawn policy, mission assignment, difficulty knobs. |
| `06_squad_mission_catalog.md` | Bounded mission catalog by squad/team type. |
| `07_squad_leader_task_state_machines.md` | Squad Leader state machines and task conversion rules. |
| `08_member_role_action_and_reaction_trees.md` | Member role action catalogs and deterministic reaction trees. |
| `09_front_hardpoint_supply_contact_integration.md` | Front, trench, hardpoint, supply, contact, visibility, and reservation integration. |
| `10_telemetry_debug_ui_and_playtest_tools.md` | Debug overlay, telemetry event names, explainability strings. |
| `11_implementation_gates.md` | Small implementation gates with files touched, tests, acceptance criteria, rollback risks. |
| `12_tests_smokes_and_acceptance_criteria.md` | Deterministic smoke tests and manual Play Mode checks. |
| `13_open_questions_and_risk_register.md` | Open design questions, risk register, recommended next decision before coding. |

## Recommended reading order

1. `01_current_system_analysis.md`
2. `02_command_hierarchy_architecture.md`
3. `03_data_contracts_and_state_model.md`
4. `04_player_general_mission_assignment.md`
5. `05_enemy_general_spawn_tasking_difficulty.md`
6. `06_squad_mission_catalog.md`
7. `07_squad_leader_task_state_machines.md`
8. `08_member_role_action_and_reaction_trees.md`
9. `09_front_hardpoint_supply_contact_integration.md`
10. `10_telemetry_debug_ui_and_playtest_tools.md`
11. `11_implementation_gates.md`
12. `12_tests_smokes_and_acceptance_criteria.md`
13. `13_open_questions_and_risk_register.md`

## Executive summary

The safest path is to add a **command layer above the existing war simulation without breaking current combat**. Keep `WarTeamSlice`, `WarFrontAssignmentPlanner`, `WarTeam`, `WarSubUnit`, and the existing enums as the simulation authority. Add a `WarCommandDirector` that owns a `PlayerGeneral`, `EnemyGeneral`, mission registry, reservation/claim registry, and command event log. In Phase 1, squads receive bounded `WarSquadMission` records, but existing team decision logic continues to perform movement/contact/combat. Then, gate by gate, move broad local decisions into `SquadMissionController`, `SquadLeaderBrain`, and `MemberTaskController`. The enemy should become an RTS-style opponent with a virtual supply/pressure budget, difficulty profiles, fair information limits, and readable spawn reasons rather than a direct “player spawned, enemy replies” prototype.

## One-page implementation roadmap

### Gate 1 — Shadow command contracts and event log

Add mission/difficulty/task/claim/event data contracts and a compact command event log. Attach a current-mission field to `WarTeam` or a sidecar command state map, but do not change squad behavior yet. This gate proves serialization, deterministic IDs, debug strings, and safe observability.

### Gate 2 — Player General mission assignment on spawn

Route player UI spawns through `PlayerGeneral.AssignMissionForNewSquad(...)` after `IntegratedPrototypeSystems.SpawnWarTeam(...)`. Existing `WarOrder` still seeds behavior. Add mission scoring and debug reasons. This gate should visibly label squads with missions but should not require full member task execution.

### Gate 3 — Debug overlay and telemetry

Give Bob a selected-squad command panel: mission, mission reason, leader task state, current order, contact state, support request, retask cooldown, and recent command events. Also add a debug-only enemy director panel after Enemy General exists.

### Gate 4 — Squad mission controller

Add `SquadMissionController` as the bridge between assigned mission and existing `TeamDecisionKind`. It should influence the existing decision selection, not replace it all at once. Example: a `BuildConnectTrench` mission biases decisions toward `ConnectTrenches`, `DigIn`, `ImprovePosition`, or `Stall` with explainable reasons.

### Gate 5 — Reservation/claim registry

Prevent chaos by adding deterministic claim tokens for hardpoints, trench sockets, support requests, and build tasks. Start with hardpoint build and occupancy claims only. Keep TTLs short and visible in debug.

### Gate 6 — Enemy General replacement

Replace the delayed enemy-response prototype with `EnemyGeneral` virtual budget, spawn cadence, lane scoring, mission assignment, and difficulty profiles. Keep “response to player pressure” behavior, but make it budgeted, capped, explainable, and testable.

### Gate 7 — Member task shadow mode, then active mode

Add member task records and per-role action catalogs. At first, record intended tasks for debug only. Then allow a small subset of tasks to affect posture/movement/working state for scouts, riflemen, sappers, medics, and porters.

### Gate 8 — Expand team templates and hardpoint families slowly

Use the 50 planned templates as a shelf, not immediate scope. Add MG, aid, mortar, command/signals, and special support teams only after the mission/task stack is stable for the existing four live templates.

## Non-goals

- No production C# implementation.
- No art generation.
- No ML/LLM runtime behavior inside the game.
- No cloud services.
- No real-world tactical instruction.
- No attempt to activate all 50 planned squad templates at once.
<!-- END FILE: 00_readme_and_package_manifest.md -->

<!-- BEGIN FILE: 01_current_system_analysis.md -->
# 01 — Current System Analysis

## Scope

This analysis separates confirmed current-code facts from the planning prompt, preservation guidance, recommended refactors, and risks. The actual Unity project was not inspected in this package pass. The facts below come from the supplied TWB Trenchworks planning prompt and should be verified by a Codex worker against the repository before coding.

---

## Confirmed current-code facts

### Project and docs locations

The current live project is listed as:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

The relevant docs folder is listed as:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs
```

Useful existing docs to read before implementation:

```text
docs/trenchworks-unit-tactics-implementation-fix-plan.md
docs/trenchworks-unit-and-squad-expansion-design.md
docs/trenchworks-phase-1-combat-expansion-master-plan-v1.md
docs/phase1-front-establishment-gate-00-master-plan.md
docs/phase1-squad-unit-local-wiki.md
docs/gpt-pro-unit-tactics-doctrine-output-intake-2026-05-17.md
docs/gpt-pro-unit-tactics-doctrine-research-prompt.md
```

Do not modify raw GPT Pro source packages if they exist in `memory/raw` or project docs.

### Existing simulation files to respect

```text
Assets/Scripts/Simulation/TrenchworksSimulation.cs
Assets/Scripts/Simulation/IntegratedPrototypeSystems.cs
Assets/Scripts/Simulation/War/WarTeamTypes.cs
Assets/Scripts/Simulation/War/WarTeamEntities.cs
Assets/Scripts/Simulation/War/WarTeamSlice.cs
Assets/Scripts/Simulation/War/WarFrontAssignment.cs
Assets/Scripts/Simulation/War/WarIntegrationFacade.cs
Assets/Scripts/Simulation/War/WarSquadAndHardpointCatalog.cs
Assets/Scripts/Unity/PrototypeBootstrap.cs
```

### Existing enum vocabulary to preserve

```text
WarTeamFaction: Player, Enemy
WarTeamKind: Scout, Assault, FortifyEngineer, Supply, Aid, MachineGun, Mortar, Command
WarOrder: Scout, Assault, Fortify, Supply, ConnectTrenches, Hold, Regroup
WarPosture: HeadUp, Crouched, Pinned, Prone, BracedWorking, DugIn
ContactState: None, Suspected, Confirmed, Held, Consolidated
```

The project already has 33 `WarMemberRole` values, including `PatrolCorporal`, `Scout`, `Rifleman`, `Sapper`, `CombatMedic`, `QuartermasterRunner`, `Porter`, `FieldEngineer`, `MgGunner`, `Grenadier`, `Signaller`, `ArtilleryObserver`, `TrenchMarksman`, `WireCutter`, `WireLayer`, `StretcherBearer`, `FieldDoctor`, `TrenchMortarCrew`, `TrenchLieutenant`, `PressureProjector`, `AetherLampScout`, `ClockworkTrenchhand`, `GraveSaltWarden`, `EchoRunner`, and `BoundShellCantor`.

Existing team decision vocabulary:

```text
TeamDecisionKind:
  Scout, Attack, Suppress, Bound, Flank, Occupy, DigIn,
  ImprovePosition, BuildHardpoint, RequestSupport, Resupply,
  TreatCasualty, ConnectTrenches, Hold, Withdraw, Regroup,
  MarkUnresolved, Stall

HoldReason:
  FiringFromPosition, Suppressing, Observing, PinnedTakingCover,
  WaitingForSupport, GuardingLine, RecoveringCohesion,
  TreatingCasualty, OutOfAmmo, NoSafePath

ContactActionKind:
  Fire, Suppress, ShiftSocket, Bound, Flank, Assault,
  RequestSupport, MarkUnresolved, Withdraw, Dig, Regroup

TeamTacticalPhase:
  MovingToLine, Occupying, Digging, Improving, InContact,
  Suppressing, Bounding, Flanking, Assaulting, Consolidating,
  RequestingSupport, Resupplying, Treating, Withdrawing,
  Regrouping, Pinned, Unresolved, Stalled
```

These are already strong building blocks. The recommended architecture should reuse them wherever possible.

### Current live spawn/interface flow

```text
WAR tray button
  -> PrototypeBootstrap.SpawnWarTeamFromInterface(...)
    -> TrenchworksSimulation.SpawnPlayerWarTeamFromInterface(...)
      -> IntegratedPrototypeSystems.SpawnWarTeam(templateId, faction, zone, order)
```

Current live templates include:

```text
scout_patrol
assault_section
fortify_engineers
supply_team
```

The current enemy-general prototype inside `TrenchworksSimulation` queues a delayed enemy response when the player spawns a squad. This is intentionally first-slice logic and should be replaced or expanded by the planned system.

### Current squad/team loop

```text
WarTeamSlice.Tick()
  -> ages contact heat
  -> detects contacts
  -> ensures front assignments
  -> updates front establishment progress
  -> chooses and applies a TeamDecision for each team
```

`WarTeamSlice.ChooseDecisionCore(...)` currently behaves like the local squad/team brain. `WarFrontAssignmentPlanner` currently assigns squads to front/support/rear/hardpoint targets.

`WarTeam` stores order, target, morale, cohesion, supply, last tactical phase, last hold/contact action, support request memory, active front blueprint claim, and recent decision history. `WarSubUnit` stores individual member role, position, health, morale, posture, leader flag, and movement/combat state.

### Current planned roster and hardpoint context

`WarSquadAndHardpointCatalog.CreatePlannedSquadTemplates()` contains 50 candidate planned squad templates. Hardpoint families include rifle/firing bay, front-line empty MG point, mortar pit, aid/doctor point, supply cache/depot, observation/signals, obstacle/wire/mines, engineering workshop/dugout, command dugout, sanitation/sustainment, occult/ward support, and breach/pressure socket.

Recommendation: keep the 50 planned templates as a **design shelf**. Do not make them immediate implementation scope.

---

## What should remain as-is

### Simulation authority stays in C#

Keep the C# war simulation as the only authority for spawning entities, ticking squads and members, front assignment, contact heat, hardpoint/trench claim state, movement, combat, posture, supply effects, mission/task transitions, and deterministic random seeds. Rendering and UI may display state and debug reasons. They should not decide combat or mission outcomes.

### Preserve current public spawn API

Keep:

```text
IntegratedPrototypeSystems.SpawnWarTeam(templateId, faction, zone, order)
TrenchworksSimulation.SpawnPlayerWarTeamFromInterface(...)
PrototypeBootstrap.SpawnWarTeamFromInterface(...)
```

Do not break the WAR tray. Add command assignment after spawn rather than replacing the user-facing spawn flow.

### Preserve current enums as low-level vocabulary

Keep the existing enum names and use them as the vocabulary below the command layer. Add only higher-level mission/task enums where the current vocabulary is too low-level.

### Preserve `WarTeamSlice.Tick()` as the simulation tick entry point

Do not immediately replace `WarTeamSlice.Tick()`. Instead, add mission state to `WarTeam` or a command-side state map, let `WarTeamSlice.Tick()` query a mission controller, and have the mission controller bias or provide context to `ChooseDecisionCore(...)`.

### Preserve `WarFrontAssignmentPlanner`

It already assigns squads to front/support/rear/hardpoint targets. The new command layer should call into it, constrain it, or consume its outputs. Do not fork a second unrelated front assignment system.

---

## What should be refactored

| Concern | Current likely location | Recommended owner |
|---|---|---|
| Delayed enemy response after player spawn | `TrenchworksSimulation` prototype logic | `EnemyGeneral` inside `WarCommandDirector` |
| Player squad mission assignment | implicit via `WarOrder`/front planner | `PlayerGeneral` |
| Enemy spawn cadence and pressure budget | prototype response logic | `EnemyGeneral` |
| Difficulty tuning | likely ad hoc or not centralized | `EnemyDifficultyProfile` |
| Strategic event log | decision history only or absent | `WarCommandDirector` command log |
| Retask policy | local / implicit | `PlayerGeneral` and `EnemyGeneral` with cooldowns |

Move mission-level choices into `SquadMissionController`; move task orchestration into `SquadLeaderBrain`; move member-role behavior into `MemberTaskController`.

---

## What should be data-driven now vs hardcoded in Phase 1

### Data-driven now

Use small static catalogs for mission catalog, allowed team kinds per mission, mission priority weights, difficulty profiles, member role action catalogs, reaction priority order, hardpoint family compatibility, claim token TTLs, and debug event names. These can be C# static data in Phase 1. They do not need ScriptableObjects immediately unless the project already uses that pattern.

### Hardcoded for Phase 1

Keep exact scoring formula weights, first four live template mappings, first difficulty profile constants, exact retask cooldown durations, first hardpoint reservation rules, minimal support request scoring, and fallback decision logic hardcoded inside small named classes. A giant method inside `TrenchworksSimulation` or `WarTeamSlice` is not acceptable.

---

## Current pain points and coupling risks

| Pain point | Risk | Recommended fix |
|---|---|---|
| `ChooseDecisionCore(...)` is doing too much | Mission, contact, supply, front assignment, and hardpoints become one monolith | Feed it mission context first; gradually split responsibilities. |
| Enemy response is tied to player spawn event | Feels like instant unfair countering | Route pressure events through `EnemyGeneral` budget, delay, caps, and info rules. |
| `WarOrder` is too low-level | `Assault` can mean many different missions | Use `WarOrder` as coarse seed, then assign `WarSquadMissionType`. |
| No bounded mission/task catalog | Behavior sprawls into special cases | Force every behavior through Mission -> Leader State -> Member Task -> Action/Reaction. |
| Hardpoint/socket conflicts | Many squads choose the same target | Add `CommandClaimToken` registry. |
| Hidden state is invisible | Bob cannot see why squads stall or retask | Add command event log and selected-squad debug strings early. |

---

## Recommended first safe implementation gate

Add data contracts and debug event logging in shadow mode. Do not change squad behavior.

Minimum safe result:

- `WarSquadMission` exists.
- `EnemyDifficultyProfile` exists.
- `CommandEventLogEntry` exists.
- Spawned squads can display “no active mission” or a temporary mission label.
- Existing `WarTeamSlice` decisions still run unchanged.
- The WAR tray still works.
- Existing smoke tests still pass.
<!-- END FILE: 01_current_system_analysis.md -->

<!-- BEGIN FILE: 02_command_hierarchy_architecture.md -->
# 02 — Command Hierarchy Architecture

## Design target

The command system should separate strategic spawn/pressure policy, operational squad mission assignment, tactical squad leader state, and individual member tasks/reactions. The current simulation remains authoritative. The command layer should be deterministic, bounded, inspectable, and testable.

---

## Proposed hierarchy

```text
WarCommandDirector
  ├─ PlayerGeneral
  │   └─ assigns missions to player squads after UI spawn
  ├─ EnemyGeneral
  │   ├─ owns virtual supply/pressure budget
  │   ├─ decides spawn cadence and team kind
  │   └─ assigns enemy missions after spawn
  ├─ SquadMissionController
  │   └─ maps mission state to squad-level tasks / TeamDecisionKind bias
  ├─ SquadLeaderBrain
  │   └─ converts squad mission into member tasks and support requests
  ├─ MemberTaskController
  │   └─ applies role action/reaction trees to WarSubUnit members
  ├─ CommandClaimRegistry
  │   └─ manages target/socket/hardpoint/support reservation tokens
  └─ CommandEventLog
      └─ stores explainable command events for UI/debug/tests
```

---

## Component definitions

### `WarCommandDirector`

Owns the command layer for both factions and coordinates command updates with the war simulation tick.

Should own:

- `PlayerGeneral`
- `EnemyGeneral`
- `SquadMissionController`
- `SquadLeaderBrain`
- `MemberTaskController`
- `CommandClaimRegistry`
- `CommandEventLog`
- command tick sequencing
- deterministic command RNG, if needed

Should not own rendering, UI input, combat resolution, physical movement, actual entity creation internals, or factory systems.

Recommended placement:

```text
Assets/Scripts/Simulation/War/Command/WarCommandDirector.cs
```

If the project avoids subfolders, place it under `Assets/Scripts/Simulation/War/` with a `WarCommand` prefix.

### `PlayerGeneral`

Assigns newly spawned player squads to missions and retasks them when the front state changes.

Inputs:

- spawned `WarTeam`
- selected entry lane / zone
- initial `WarOrder`
- player doctrine
- current front state
- hardpoint/trench availability
- active contacts
- support requests
- supply/casualty pressure
- command claim registry

Outputs:

- `WarSquadMission`
- mission score breakdown
- claim token for mission target, if needed
- command event log entries

Agency boundary: the player chooses what to spawn, when to spawn, selected lane/zone, doctrine if available, and broad intent. The Player General chooses the battlefield mission, target front depth/hardpoint/support request, and retask timing.

### `EnemyGeneral`

Acts like an RTS skirmish opponent with no physical factory.

Owns:

- virtual supply/pressure budget
- spawn cadence
- response delay
- difficulty profile
- team cap
- lane scoring
- counter-pick logic
- escalation over time
- enemy mission assignment
- fair information limitations

Does not own player factory, player resources, combat result forcing, or hidden UI/minimap leaks.

### `SquadMissionController`

Tracks mission status for each squad and converts mission goals into tactical decision context.

```text
WarSquadMission
  -> mission status / phase
    -> preferred TeamDecisionKind outputs
      -> existing WarTeamSlice decision logic
```

It should be introduced before member tasks become active.

### `SquadLeaderBrain`

Converts a squad mission into squad-level task states and member assignments.

Owns:

- local squad blackboard
- task state machine
- support request decisions
- leader-down fallback
- mission completion/failure checks
- per-member task assignment requests

Reads `WarTeam`, `WarSubUnit`, `WarSquadMission`, local contacts, local supply state, local hardpoint/trench socket state, and command claims.

### `MemberTaskController`

Applies role-specific task catalogs and deterministic reaction trees. It owns member task state, reaction trigger evaluation, role action selection, and task completion/failure reports. It does not choose global missions, enemy spawns, or front plans.

---

## Decision ownership by layer

| Layer | Scope | Owner | Examples |
|---|---|---|---|
| Strategic | Faction-wide pressure, difficulty, spawn budget | `EnemyGeneral`, limited PlayerGeneral policy | Enemy spawn timing, lane pressure response, escalation. |
| Operational | Which squad should do which mission | `PlayerGeneral`, `EnemyGeneral` | Scout lane B, engineer builds MG point, supply answers ammo request. |
| Tactical | How a squad executes the mission | `SquadMissionController`, `SquadLeaderBrain` | Move, occupy, dig, resupply, treat, regroup. |
| Individual | What a member does this tick/task phase | `MemberTaskController` | Scout observes, sapper works socket, medic treats, porter carries. |
| Physical simulation | Movement, contact, posture, supply, combat application | Existing war simulation / `WarTeamSlice` | Detect contact, update posture, apply supply, progress trench work. |

---

## Player button spawn sequence

```text
Bob presses WAR tray button
  |
  v
PrototypeBootstrap.SpawnWarTeamFromInterface(templateId, selectedLane, order)
  |
  v
TrenchworksSimulation.SpawnPlayerWarTeamFromInterface(templateId, selectedLane, order)
  |
  v
IntegratedPrototypeSystems.SpawnWarTeam(templateId, WarTeamFaction.Player, zone, order)
  |
  v
WarTeam created with WarTeamKind, members, order, target seed
  |
  v
WarCommandDirector.OnWarTeamSpawned(teamId, source = PlayerInterface)
  |
  v
PlayerGeneral.AssignMissionForNewSquad(team, selectedLane, order, doctrine, frontSnapshot)
  |
  v
Mission candidates scored against front/contact/hardpoint/support/supply state
  |
  v
Best WarSquadMission assigned
  |
  v
Optional CommandClaimToken reserved
  |
  v
CommandEventLog records:
  Command.PlayerSquadSpawned
  Command.MissionAssigned
  Command.AssignmentReason
  |
  v
WarTeamSlice.Tick() continues normal simulation
  |
  v
SquadMissionController reads mission and biases squad decisions
```

Player spawn rule: do not prevent the player from spawning a squad because the general cannot find a perfect mission. Assign a fallback mission such as `HoldFightingLine`, `RegroupWithdraw`, `ScoutProbe`, or `ReserveHold` depending on team kind.

---

## Enemy response spawn sequence

```text
War simulation tick
  |
  v
WarCommandDirector.TickCommandLayer(simTick)
  |
  v
EnemyGeneral.UpdateVirtualBudget(time, pressureEvents, difficulty)
  |
  v
EnemyGeneral.CheckSpawnEligibility()
  |
  +-- if not eligible:
  |      record no event unless debug detail enabled
  |
  +-- if eligible:
         |
         v
     EnemyGeneral.ScoreLaneNeeds(frontSnapshot, knownPlayerPressure, difficultyInfoRules)
         |
         v
     EnemyGeneral.SelectTeamKind(enemyRosterShelf, budget, cap, pressure, techTier)
         |
         v
     IntegratedPrototypeSystems.SpawnWarTeam(templateId, WarTeamFaction.Enemy, enemyZone, seedOrder)
         |
         v
     EnemyGeneral.AssignMissionForNewEnemySquad(team, lane, pressureReason)
         |
         v
     CommandClaimRegistry reserves mission target if needed
         |
         v
     CommandEventLog records:
       Command.EnemySpawnQueued
       Command.EnemySpawned
       Command.MissionAssigned
       Command.EnemySpawnReason
         |
         v
     WarTeamSlice.Tick() executes the spawned team through normal simulation
```

Enemy response rule: the enemy may respond to player pressure, but the response must be mediated by budget, delay, cap, difficulty, lane choice, information rules, cooldown, and an explainable reason.

---

## Mission assignment lifecycle

```text
No Mission
  |
  | On team spawned or loaded without mission
  v
Candidate Missions Built
  |
  | Score mission candidates
  v
Mission Assigned
  |
  | Claim target if needed
  v
Mission Active
  |
  +--> Completed
  |      |
  |      v
  |   Follow-up mission or Hold/Reserve
  |
  +--> Failed
  |      |
  |      v
  |   Regroup / Support Request / Retask
  |
  +--> Retask Requested
         |
         | Cooldown clear and better mission score exists
         v
      Mission Replaced
```

Recommended mission statuses:

```text
Pending
Assigned
Active
Paused
Completed
Failed
Retasking
Cancelled
```

---

## Re-tasking lifecycle

```text
Mission Active
  |
  v
Retask trigger observed?
  |
  +-- no --> Continue mission
  |
  +-- yes
       |
       v
   Is mission lockout/cooldown active?
       |
       +-- yes --> Record RetaskBlocked, continue or pause
       |
       +-- no
            |
            v
        Build candidate replacement missions
            |
            v
        Is replacement score meaningfully higher?
            |
            +-- no --> Continue mission, record reason if debug selected
            |
            +-- yes
                 |
                 v
             Release old claim token
                 |
                 v
             Assign replacement mission
                 |
                 v
             Record MissionRetasked event
```

Retask triggers should be bounded: assigned hardpoint complete, socket invalid, no safe path, pinned too long, low ammo, casualties, leader down, nearby support request outranks current mission, contact escalates, front lane collapses/over-saturates, or success condition met.

Retasking should require a valid trigger, expired cooldown, replacement mission score above the current mission by a margin, and no critical local reaction in progress unless the new mission is emergency regroup/medical/resupply.

---

## Command tick order recommendation

```text
1. Existing simulation pre-update as needed.
2. Command layer observes front/contact/supply snapshot.
3. EnemyGeneral updates budget and may queue/spawn.
4. PlayerGeneral processes newly spawned player squads.
5. Generals evaluate limited retasks.
6. SquadMissionController updates mission states.
7. SquadLeaderBrain updates squad task states.
8. MemberTaskController updates member tasks/reactions.
9. WarTeamSlice applies physical squad decisions.
10. CommandEventLog prunes old debug entries.
```

If current `WarTeamSlice.Tick()` must remain earlier in the call order, start in shadow mode and only write mission labels.

---

## Anti-monolith boundaries

Do not create a method like:

```text
UpdateAllAIAndMissionAndEnemySpawnAndMemberTasks(...)
```

Even in a small Phase 1, `WarCommandDirector`, `PlayerGeneral`, `EnemyGeneral`, `CommandEventLog`, and `CommandCatalogs` should be separate files or clearly separate classes.

---

## Determinism boundary

The command hierarchy should be replay-friendly:

- no unseeded random calls
- no dependency on wall-clock time
- stable sort tie-breakers
- stable team/member IDs
- command events use sim tick, not `DateTime`
- claim tokens expire by sim tick, not seconds
- difficulty profile loaded once per scenario unless deliberately changed

---

## Recommended first architecture implementation

Add:

```text
WarCommandDirector
PlayerGeneral
EnemyGeneral stub
CommandEventLog
WarSquadMission
EnemyDifficultyProfile
```

Wire only this path first:

```text
player spawn
  -> OnWarTeamSpawned
    -> assign shadow mission
      -> event log
        -> selected-squad debug label
```

No behavior changes yet.
<!-- END FILE: 02_command_hierarchy_architecture.md -->

<!-- BEGIN FILE: 03_data_contracts_and_state_model.md -->
# 03 — Data Contracts and State Model

## Purpose

This file proposes the minimum data contracts needed to support Player General mission assignment, Enemy General virtual budget/spawn policy/difficulty, squad mission state, squad leader task state, member task state, reaction trees, target reservations, and command event logging.

These are C#-style planning contracts, not production code.

---

## Existing enums to reuse

| Existing enum | Reuse for |
|---|---|
| `WarTeamFaction` | Command ownership: Player or Enemy. |
| `WarTeamKind` | Mission eligibility and spawn selection. |
| `WarMemberRole` | Member task/action catalog lookup. |
| `WarOrder` | Initial UI seed / coarse intent. |
| `WarPosture` | Member posture result from tasks/reactions. |
| `ContactState` | Contact escalation and mission triggers. |
| `TeamDecisionKind` | Squad-level output/bias from missions. |
| `HoldReason` | Explanation for hold/stall/pinned/resupply/treating states. |
| `ContactActionKind` | Local contact reaction summary. |
| `TeamTacticalPhase` | Squad tactical phase and debug display. |
| `WarSupportRequestKind` | Support requests: Ammo, Engineer, FireSupport, Medical, Regroup. |

Do not duplicate these with parallel command enums unless the current enum cannot express the needed higher-level concept.

---

## New enums recommended

### `WarSquadMissionType`

```csharp
public enum WarSquadMissionType
{
    None = 0,
    ScoutProbe,
    MarkContact,
    ScreenFlank,
    AssaultLine,
    HoldFightingLine,
    OccupyRifleBay,
    DigIn,
    ImproveTrench,
    BuildConnectTrench,
    ClaimBuildMgPoint,
    MortarSupport,
    CommandRelay,
    SupplyResupply,
    CasualtyResponse,
    RegroupWithdraw,
    ReserveHold
}
```

### `WarMissionStatus`

```csharp
public enum WarMissionStatus
{
    Pending,
    Assigned,
    Active,
    Paused,
    Completed,
    Failed,
    Retasking,
    Cancelled
}
```

### `WarMissionPriority`

```csharp
public enum WarMissionPriority
{
    Low,
    Normal,
    High,
    Emergency
}
```

### `WarGeneralIntent`

```csharp
public enum WarGeneralIntent
{
    Balanced,
    ReconFirst,
    HoldGround,
    BuildDepth,
    AggressivePressure,
    SustainAndRecover,
    CounterAttack,
    Attrition
}
```

### `EnemyDifficultyTier`

```csharp
public enum EnemyDifficultyTier
{
    Recruit,
    Regular,
    Veteran,
    Brutal
}
```

### `EnemyInfoAccessLevel`

```csharp
public enum EnemyInfoAccessLevel
{
    VisibleOnly,
    RecentContactMemory,
    PressureApproximation,
    WeightedOmniscienceLite
}
```

### `MemberTaskType`

```csharp
public enum MemberTaskType
{
    None,
    MoveToSquadTarget,
    MoveToSocket,
    HoldCover,
    ObserveArc,
    MarkContact,
    FireAtContact,
    SuppressContact,
    BoundMove,
    RegroupOnLeader,
    WithdrawToSafePoint,
    DigTrench,
    ImproveTrench,
    BuildHardpoint,
    RepairHardpoint,
    ClearObstacle,
    PlaceObstacle,
    CarrySupply,
    ResupplySquad,
    FetchAmmo,
    TreatWounded,
    CarryStretcher,
    OperateMachineGun,
    OperateMortar,
    SpotForSupport,
    RelayCommand,
    GuardWorker,
    GuardMedic,
    IdleReserve
}
```

### `MemberTaskStatus`

```csharp
public enum MemberTaskStatus
{
    Unassigned,
    Assigned,
    Moving,
    Working,
    Waiting,
    Blocked,
    Completed,
    Failed,
    Interrupted
}
```

### `ReactionTrigger`

```csharp
public enum ReactionTrigger
{
    None,
    BeingAttacked,
    EnemySeen,
    EnemyHeard,
    SuppressionTaken,
    Wounded,
    LowAmmo,
    LowFood,
    LowMedical,
    NoSafePath,
    LeaderDown,
    MissionTargetReached,
    HardpointSocketReached,
    TrenchSocketReached,
    BuildTaskAssigned,
    RetreatOrdered,
    RegroupOrdered
}
```

### `ReactionPolicy`

```csharp
public enum ReactionPolicy
{
    Ignore,
    ReportOnly,
    PauseTaskThenReact,
    InterruptTask,
    OverrideUntilSafe,
    RequestLeaderDecision
}
```

### `CommandClaimKind`

```csharp
public enum CommandClaimKind
{
    MissionTarget,
    FrontAssignment,
    TrenchSocket,
    HardpointSocket,
    HardpointBuildJob,
    SupplyRequest,
    MedicalRequest,
    FireSupportRequest,
    RegroupPoint
}
```

### `CommandEventKind`

```csharp
public enum CommandEventKind
{
    PlayerSquadSpawned,
    EnemySpawnQueued,
    EnemySpawned,
    MissionCandidateScored,
    MissionAssigned,
    MissionRetasked,
    MissionCompleted,
    MissionFailed,
    ClaimCreated,
    ClaimReleased,
    ClaimExpired,
    ClaimDenied,
    SquadLeaderStateChanged,
    MemberTaskAssigned,
    MemberTaskCompleted,
    MemberTaskFailed,
    SupportRequestRaised,
    SupportRequestAccepted,
    SupportRequestCancelled,
    EnemyBudgetChanged,
    EnemySpawnBlocked,
    DifficultyProfileApplied,
    DebugNote
}
```

---

## Core records/classes

### `WarSquadMission`

```csharp
public sealed class WarSquadMission
{
    public int MissionId;
    public int TeamId;
    public WarTeamFaction Faction;
    public WarSquadMissionType Type;
    public WarMissionStatus Status;
    public WarMissionPriority Priority;

    public WarGeneralIntent Intent;
    public WarOrder SeedOrder;
    public WarTeamKind TeamKind;

    public int AssignedTick;
    public int LastUpdatedTick;
    public int RetaskLockedUntilTick;

    public string LaneId;
    public string TargetFrontId;
    public string TargetSectorId;
    public string TargetBlueprintPieceId;
    public string TargetHardpointId;
    public string TargetSocketId;

    public int ClaimTokenId;

    public float Score;
    public string AssignmentReason;
    public string RetaskReason;
    public string FailureReason;

    public TeamDecisionKind[] LikelyDecisionOutputs;
}
```

Notes: `MissionId` should be deterministic and stable for a run. Target fields can be strings initially if current IDs are string-like; otherwise use existing ID types. `ClaimTokenId` can be `0` or `-1` when no claim exists. `AssignmentReason` should be short enough for UI.

### `MissionScoreContext`

```csharp
public readonly struct MissionScoreContext
{
    public readonly int SimTick;
    public readonly WarTeamFaction Faction;
    public readonly WarTeamKind TeamKind;
    public readonly WarOrder SeedOrder;
    public readonly WarGeneralIntent Intent;
    public readonly string SelectedLaneId;
    public readonly ContactState LaneContactState;
    public readonly float LanePressure;
    public readonly float FriendlyDensity;
    public readonly float EnemyPressureEstimate;
    public readonly float SupplyPressure;
    public readonly float CasualtyPressure;
    public readonly float StalledSectorPressure;
    public readonly int EmptyHardpointSockets;
    public readonly int StartedHardpoints;
    public readonly int CompletedHardpoints;
    public readonly int OpenSupportRequests;
    public readonly bool HasSafePath;
    public readonly bool HasClaimableTarget;
}
```

### `AssignmentScoreBreakdown`

```csharp
public sealed class AssignmentScoreBreakdown
{
    public WarSquadMissionType MissionType;
    public float BaseScore;
    public float LaneScore;
    public float DoctrineScore;
    public float ContactScore;
    public float HardpointScore;
    public float SupplyScore;
    public float CasualtyScore;
    public float StallScore;
    public float ClaimPenalty;
    public float TotalScore;
    public string Reason;
}
```

The selected mission’s score breakdown should be available for debug. Full candidate lists can be kept only in debug builds or recent event logs.

---

## Enemy General contracts

### `EnemyDifficultyProfile`

```csharp
public sealed class EnemyDifficultyProfile
{
    public EnemyDifficultyTier Tier;
    public float StartingBudget;
    public float BudgetIncomePerMinute;
    public float MaxBudget;
    public int MinResponseDelayTicks;
    public int MaxResponseDelayTicks;
    public int SpawnCooldownTicks;
    public int SoftTeamCap;
    public int HardTeamCap;
    public float AggressionWeight;
    public float DefenseWeight;
    public float SupportWeight;
    public float CounterPickWeight;
    public float ComebackBudgetMultiplier;
    public float SnowballThrottleMultiplier;
    public float SupplyGenerosity;
    public float TechMixAdvanceRate;
    public EnemyInfoAccessLevel InfoAccess;
    public float InformationNoise;
    public bool CanUseRecentUnseenContactMemory;
    public bool CanPrioritizeHiddenSupportRequests;
}
```

### `EnemyVirtualBudget`

```csharp
public sealed class EnemyVirtualBudget
{
    public float CurrentBudget;
    public float PressureDebt;
    public float ComebackReserve;
    public int LastIncomeTick;
    public int LastSpawnTick;
    public int NextAllowedSpawnTick;
    public string LastBudgetReason;
}
```

### `EnemySpawnCandidate`

```csharp
public sealed class EnemySpawnCandidate
{
    public string TemplateId;
    public WarTeamKind TeamKind;
    public WarOrder SeedOrder;
    public string LaneId;
    public WarSquadMissionType MissionType;
    public float Cost;
    public float Score;
    public string Reason;
}
```

---

## Squad Leader contracts

```csharp
public enum SquadLeaderTaskState
{
    None,
    MovingToAssignment,
    OccupyingPosition,
    FightingFromPosition,
    OpenGroundContact,
    BuildingTrench,
    ImprovingTrench,
    ClaimingHardpoint,
    Resupplying,
    MedicalResponse,
    Retreating,
    Regrouping,
    LeaderDownFallback,
    Stalled
}
```

```csharp
public sealed class SquadBlackboard
{
    public int TeamId;
    public int ActiveMissionId;
    public SquadLeaderTaskState LeaderState;
    public ContactState LocalContactState;
    public string LocalContactId;
    public string CurrentCoverSocketId;
    public string CurrentHardpointId;
    public bool IsPinned;
    public bool HasLowAmmo;
    public bool HasCasualty;
    public bool LeaderIsDown;
    public bool HasSafePath;
    public int LastStateChangeTick;
    public int LastSupportRequestTick;
    public int LastMemberTaskAssignTick;
    public string StateReason;
}
```

---

## Member task contracts

```csharp
public sealed class MemberTask
{
    public int TaskId;
    public int TeamId;
    public int MemberId;
    public WarMemberRole Role;
    public MemberTaskType Type;
    public MemberTaskStatus Status;
    public int AssignedTick;
    public int StartedTick;
    public int CompletedTick;
    public int ExpiresTick;
    public string TargetSocketId;
    public string TargetHardpointId;
    public string TargetContactId;
    public string TargetMemberId;
    public ReactionPolicy InterruptionPolicy;
    public string AssignmentReason;
    public string FailureReason;
}
```

```csharp
public sealed class MemberReactionRule
{
    public WarMemberRole Role;
    public ReactionTrigger Trigger;
    public ReactionPolicy Policy;
    public MemberTaskType PreferredTask;
    public TeamDecisionKind? SquadDecisionHint;
    public HoldReason? HoldReasonHint;
    public int Priority;
    public string DebugText;
}
```

---

## Claim/reservation contracts

```csharp
public sealed class CommandClaimToken
{
    public int ClaimTokenId;
    public CommandClaimKind Kind;
    public WarTeamFaction Faction;
    public int TeamId;
    public int MissionId;
    public string TargetId;
    public string TargetLaneId;
    public string TargetSectorId;
    public int CreatedTick;
    public int ExpiresTick;
    public int LastRenewedTick;
    public bool IsShared;
    public int MaxSharedUsers;
    public string Reason;
}
```

| Claim kind | Default sharing | Notes |
|---|---:|---|
| `MissionTarget` | Usually exclusive | Prevents many squads choosing the same small objective. |
| `FrontAssignment` | Shared by density limit | Several squads can hold a lane, but cap density. |
| `TrenchSocket` | Exclusive | One squad/member work group per small socket. |
| `HardpointSocket` | Exclusive unless hardpoint supports crew slots | MG/mortar/aid sockets define slot count. |
| `HardpointBuildJob` | Exclusive | One engineer crew owns build progress unless assisted intentionally. |
| `SupplyRequest` | One primary responder, optional backup | Prevents every supply team chasing same request. |
| `MedicalRequest` | One primary responder, optional stretcher support | Prevents duplicate medics. |
| `FireSupportRequest` | Shared by support capacity | Mortar/observer logic can be capacity-based. |
| `RegroupPoint` | Shared | Multiple members/squads can regroup. |

---

## Command event log

```csharp
public sealed class CommandEventLogEntry
{
    public int EventId;
    public int SimTick;
    public CommandEventKind Kind;
    public WarTeamFaction Faction;
    public int TeamId;
    public int MissionId;
    public int MemberId;
    public int ClaimTokenId;
    public string LaneId;
    public string TargetId;
    public string Summary;
    public string Detail;
    public float Score;
    public string ReasonCode;
}
```

Example event summaries:

```text
MissionAssigned: Team 14 ScoutProbe lane=North score=83 reason=SelectedLane+NoContact+NeedVisibility
EnemySpawned: Enemy Assault lane=Center mission=HoldFightingLine reason=PlayerPressureHigh budget=42
ClaimDenied: Team 7 hardpoint=MG_A3 reason=AlreadyClaimedByTeam12
MemberTaskFailed: Team 3 member=Porter task=CarrySupply reason=NoSafePath
```

Use fixed ring buffers:

```text
global command log: latest 256 events
per-team command log: latest 16 events
per-member command log: latest 8 events
```

---

## Serialization and determinism notes

Save only stable state: active missions, active claims, enemy virtual budget, difficulty tier/profile ID, squad blackboards, active member tasks if active mode is enabled, and compact command log only if debug save is desired. Do not save full score candidate history, temporary arrays, expired claims, debug-only candidate tables, or wall-clock timestamps.

Use schema versions:

```text
CommandStateVersion = 1
MissionSchemaVersion = 1
EnemyGeneralSchemaVersion = 1
MemberTaskSchemaVersion = 1
```

All timeouts, cooldowns, spawn delays, and claim TTLs should use simulation ticks. When two candidates tie, use stable tie-breakers: higher priority, lower friendly density, older support request, lower stable lane ID, lower team ID, then lower mission enum value. If variety is needed, use a seeded command RNG derived from run seed, sim tick bucket, faction, and lane ID.

---

## Phase 1 data-driven stance

Use static C# catalogs first:

```text
CommandMissionCatalog
EnemyDifficultyCatalog
MemberRoleActionCatalog
ReactionRuleCatalog
HardpointFamilyCompatibilityCatalog
```

Move catalogs to ScriptableObjects only after behavior is stable, Bob wants designer-editable tuning, tests cover defaults, and save-state compatibility is understood.

---

## Minimum data contracts for Gate 1

Gate 1 should add only:

```text
WarSquadMissionType
WarMissionStatus
WarMissionPriority
WarGeneralIntent
EnemyDifficultyTier
EnemyDifficultyProfile
WarSquadMission
AssignmentScoreBreakdown
CommandEventKind
CommandEventLogEntry
CommandEventLog
```

Optional in Gate 1: `CommandClaimToken`. Member task contracts should wait until the squad mission layer is visible and useful.

## Pushback

Do not add every enum and record in this file in one coding pass. The complete model is listed so the architecture stays coherent, but the first implementation gate should only add what it can test immediately.
<!-- END FILE: 03_data_contracts_and_state_model.md -->

<!-- BEGIN FILE: 04_player_general_mission_assignment.md -->
# 04 — Player General Mission Assignment

## Purpose

The Player General assigns newly spawned player squads to battlefield missions without removing player agency.

Bob/player still chooses:

- what squad to spawn
- when to spawn
- selected lane / entry zone
- broad order/doctrine, if exposed

The Player General chooses:

- the best bounded mission for that squad
- which sector/socket/hardpoint/support request the squad should serve
- whether a squad should be retasked later

The Player General should not spawn units autonomously.

---

## Entry point

Recommended hook after the existing spawn flow:

```text
PrototypeBootstrap.SpawnWarTeamFromInterface(...)
  -> TrenchworksSimulation.SpawnPlayerWarTeamFromInterface(...)
    -> IntegratedPrototypeSystems.SpawnWarTeam(templateId, Player, zone, order)
      -> WarCommandDirector.OnWarTeamSpawned(teamId, PlayerInterface)
        -> PlayerGeneral.AssignMissionForNewSquad(...)
```

Do not break the WAR tray. Do not require UI rewrite in Gate 1.

---

## Inputs to mission scoring

| Input | Source | Use |
|---|---|---|
| Team kind | `WarTeamKind` | Determines legal missions. |
| Initial order | `WarOrder` | Seeds mission preference. |
| Selected lane/zone | UI/spawn flow | Strong lane preference. |
| Front assignment availability | `WarFrontAssignmentPlanner` / snapshot | Finds valid front/support/rear/hardpoint targets. |
| Contact state | `ContactState`, contact heat | Scouts mark; assault holds/attacks; support avoids unsafe paths. |
| Hardpoint state | hardpoint/trench blueprint data | Engineers/MG/mortar/aid/supply choose build/occupy targets. |
| Supply state | `WarTeam` supply and support requests | Supply teams answer ammo/food needs. |
| Casualty pressure | team health/support requests | Aid teams answer medical needs. |
| Stalled sectors | tactical phase/history | Engineers/support/regroup target stalled lanes. |
| Friendly density | teams per lane/sector | Avoid overstacking. |
| Claims/reservations | `CommandClaimRegistry` | Avoid duplicate target assignments. |

Optional inputs: doctrine, minimap/player visibility, recent enemy pressure, trench depth, desired hardpoint family by sector.

---

## Player doctrine

If doctrine exists or is added, keep it simple.

| Doctrine / intent | Bias |
|---|---|
| `Balanced` | Normal mission weights. |
| `ReconFirst` | Scouts probe/mark; assault avoids blind attacks. |
| `HoldGround` | Assault holds; engineers improve; supply supports. |
| `BuildDepth` | Engineers connect/improve; supply prepares caches. |
| `AggressivePressure` | Assault line, scout marking, MG/mortar support later. |
| `SustainAndRecover` | Supply, casualty response, regroup, improve trench. |

If no doctrine UI exists, default to `Balanced`.

---

## Mission assignment scoring

### Basic flow

```text
1. Build mission candidates allowed for team kind.
2. Filter impossible candidates.
3. Score each candidate.
4. Apply claim/overcrowding penalties.
5. Choose highest score with stable tie-breakers.
6. Create mission.
7. Reserve claim token if target/socket/support request needs one.
8. Log assignment reason.
```

### C#-style pseudocode

```csharp
WarSquadMission AssignMissionForNewSquad(WarTeam team, SpawnContext spawn)
{
    var context = BuildMissionScoreContext(team, spawn);
    var candidates = MissionCatalog.GetAllowedMissions(team.Kind);

    AssignmentScoreBreakdown best = default;

    foreach (var candidate in candidates)
    {
        if (!IsCandidatePossible(candidate, context))
            continue;

        var score = ScoreCandidate(candidate, context);
        score.TotalScore -= ClaimPenalty(candidate, context);
        score.TotalScore -= FriendlyOverstackPenalty(candidate, context);

        best = PickBetterStable(best, score);
    }

    if (best == null)
        best = BuildFallbackMission(team, context);

    var mission = CreateMission(team, best);
    TryCreateClaim(mission);

    CommandLog.AddMissionAssigned(team, mission, best.Reason);
    return mission;
}
```

---

## Scoring components

| Component | Meaning |
|---|---|
| Base score | Default usefulness of the mission for this team kind. |
| Selected lane score | Bonus if mission uses the player-selected lane. |
| Doctrine score | Bonus from player doctrine. |
| Contact score | Bonus/penalty based on `ContactState`. |
| Hardpoint score | Bonus if matching empty/started hardpoint exists. |
| Trench depth score | Bonus for build/improve/connect where trench depth is weak. |
| Support score | Bonus for open support requests. |
| Supply score | Bonus for low-supply friendly teams. |
| Casualty score | Bonus for wounded/casualty pressure. |
| Stall score | Bonus if target lane has `Stalled`, `Pinned`, `NoSafePath`. |
| Claim penalty | Penalty if target is already reserved. |
| Density penalty | Penalty if lane/sector is overstacked. |

Example reason:

```text
mission=BuildConnectTrench score=78.5 reason=SelectedLane+WeakTrenchDepth+EmptyEngineerSocket+NoClaimConflict
```

---

## Mission rules by squad type

### Scouts — `WarTeamKind.Scout`

Primary missions:

| Mission | When to choose |
|---|---|
| `ScoutProbe` | Selected lane lacks confirmed contact and needs visibility. |
| `MarkContact` | Contact is suspected/confirmed but not consolidated. |
| `ScreenFlank` | Adjacent lane has pressure or unresolved contact. |
| `ReserveHold` | No safe path or lane is saturated. |

High-score inputs: selected lane with `ContactState.None` or `Suspected`, low visibility, unresolved/stalled sectors, observation/signals hardpoint needs. Penalize confirmed heavy pressure with no cover path, already scouted lanes, and duplicate scout claims.

Likely outputs:

```text
Scout
Occupy
Hold
MarkUnresolved
Withdraw
Regroup
```

### Assault / rifle teams — `WarTeamKind.Assault`

Primary missions:

| Mission | When to choose |
|---|---|
| `AssaultLine` | Lane has confirmed pressure and assault path exists. |
| `HoldFightingLine` | Front needs bodies to stabilize. |
| `OccupyRifleBay` | Rifle/firing bay exists or is nearly complete. |
| `RegroupWithdraw` | Team is badly depleted, pinned, or no safe path. |

High-score inputs: selected lane under moderate pressure, front sector with weak friendly density, occupied trenches/hardpoints needing defenders, confirmed contact with enough cohesion/supply. Penalize low ammo, high casualty pressure, no safe path, crowding, and duplicate hardpoint/socket claims.

Likely outputs:

```text
Attack
Suppress
Bound
Occupy
Hold
RequestSupport
Withdraw
Regroup
```

### Fortify engineers — `WarTeamKind.FortifyEngineer`

Primary missions:

| Mission | When to choose |
|---|---|
| `DigIn` | Front position lacks cover. |
| `ImproveTrench` | Existing trench depth or quality is weak. |
| `BuildConnectTrench` | Two friendly positions need connection. |
| `ClaimBuildMgPoint` | Empty MG hardpoint socket exists and front needs fire support. |
| `ReserveHold` | No valid build job exists yet. |

High-score inputs: selected lane with empty/started hardpoints, weak trench depth, front establishment progress needing work, hardpoint family requests, stalled sectors caused by `NoSafePath` or lack of cover. Penalize confirmed contact unless protected, duplicate build claims, no path, and sector too far from supply.

Likely outputs:

```text
DigIn
ImprovePosition
BuildHardpoint
ConnectTrenches
Hold
RequestSupport
Withdraw
Regroup
Stall
```

### Supply teams — `WarTeamKind.Supply`

Primary missions:

| Mission | When to choose |
|---|---|
| `SupplyResupply` | Ammo/supply support request exists. |
| `ReserveHold` | No request exists; hold near supply route/cache. |
| `RegroupWithdraw` | Supply team threatened or no safe route. |

High-score inputs: oldest high-priority ammo request, low-supply assault/MG/mortar/engineer team, selected lane support request, completed/planned supply cache, teams with `HoldReason.OutOfAmmo`. Penalize unsafe routes, duplicate supply claims, already satisfied target, and overextended route with no trench connection.

Likely outputs:

```text
Resupply
Hold
RequestSupport
Withdraw
Regroup
Stall
```

### Future MG teams — `WarTeamKind.MachineGun`

Primary missions:

| Mission | When to choose |
|---|---|
| `OccupyRifleBay` | Temporary fighting position before MG point. |
| `ClaimBuildMgPoint` | If MG point exists and needs crew; engineers may build, MG crew occupies. |
| `HoldFightingLine` | Lane needs suppression/defense. |
| `RegroupWithdraw` | No ammo, no socket, or untenable position. |

High-score inputs: completed/started MG point, lane with confirmed pressure, supply route available, observation/contact support, friendly assault nearby. Penalize no ammo support, no socket, too-mobile missions, and no safe path.

### Future mortar teams — `WarTeamKind.Mortar`

Primary missions: `MortarSupport`, temporary support position, `ReserveHold`, `RegroupWithdraw`. Require mortar pit/position, fire support request or marked contact, and supply availability. Penalize no spotter/request and low supply.

### Future aid / medical teams — `WarTeamKind.Aid`

Primary missions: `CasualtyResponse`, `ReserveHold`, `RegroupWithdraw`. High-score inputs are medical requests, casualty pressure, aid/doctor hardpoint, and safe trench route. Penalize duplicate medical responder and unsafe path.

### Future command/signals teams — `WarTeamKind.Command`

Primary missions: `CommandRelay`, `ReserveHold`, `MarkContact` if signallers/observers can help, and `RegroupWithdraw`. High-score inputs are missing command coverage, support chain failures, observation/signals hardpoint, and stalled sectors from poor support routing.

---

## Retasking rules

| Trigger | Candidate replacement |
|---|---|
| Mission complete | Follow-up `HoldFightingLine`, `ReserveHold`, or next build/support mission. |
| No safe path for threshold | `RegroupWithdraw` or alternate lane mission. |
| Low ammo | `RequestSupport` state or `RegroupWithdraw`. |
| High casualties | `CasualtyResponse` request or `RegroupWithdraw`. |
| Leader down | `RegroupWithdraw` or leader fallback state. |
| Assigned hardpoint already claimed/completed | New hardpoint/build/occupy mission. |
| Contact escalates | Scout -> `MarkContact`; assault -> `HoldFightingLine`/`AssaultLine`; support -> withdraw/hold. |
| Support request appears nearby | Supply/Aid/Command may retask if request outranks current mission. |
| Lane overstacked | Move to support/rear/reserve or adjacent weak sector. |
| Mission stalled too long | Re-score candidates; log stall reason. |

Use cooldowns to prevent thrashing:

| Mission class | Retask cooldown |
|---|---:|
| Scout/probe | 20-40 ticks |
| Assault/hold | 40-80 ticks |
| Build/improve | 80-160 ticks |
| Supply/medical emergency | 10-30 ticks |
| Regroup/withdraw | locked until safe or completed |

A new mission should beat the current mission by a meaningful margin before replacement: normal mission `+15`, emergency support `+5`, leader down/no safe path no margin required.

---

## Assignment examples

### Scout patrol in Center

```text
Inputs:
- TeamKind Scout
- Selected lane Center
- ContactState None
- Low visibility
- No scout claim in lane
- Doctrine Balanced

Assigned:
- Mission ScoutProbe
- Target lane Center
- Reason SelectedLane+LowVisibility+NoScoutClaim
```

### Fortify engineers in North

```text
Inputs:
- TeamKind FortifyEngineer
- Selected lane North
- Empty MG hardpoint socket
- Front has confirmed contact but assault team nearby
- No build claim

Assigned:
- Mission ClaimBuildMgPoint
- Target MG socket North-MG-01
- Reason EmptyMgPoint+FrontPressure+FriendlyCover+NoClaimConflict
```

### Supply team

```text
Inputs:
- TeamKind Supply
- Ammo request from assault team in selected lane
- Safe trench path exists
- Request unclaimed

Assigned:
- Mission SupplyResupply
- Target support request Ammo#42
- Reason AmmoRequest+SelectedLane+SafePath+OldestRequest
```

---

## Fallback missions

| Team kind | Fallback |
|---|---|
| Scout | `ScoutProbe` if safe path exists, else `ReserveHold`. |
| Assault | `HoldFightingLine` if front exists, else `ReserveHold`. |
| FortifyEngineer | `DigIn` if target exists, else `ReserveHold`. |
| Supply | `ReserveHold` near supply route/cache. |
| Aid | `ReserveHold` near aid point. |
| MachineGun | `HoldFightingLine` or `ReserveHold` if no socket. |
| Mortar | `ReserveHold` until mortar support is valid. |
| Command | `CommandRelay` if socket exists, else `ReserveHold`. |

---

## UI/debug requirement

Each mission assignment must have a short reason Bob can read.

Good examples:

```text
ScoutProbe: selected lane has low visibility and no scout assigned.
SupplyResupply: ammo request from Assault #12 is old, nearby, and unclaimed.
ClaimBuildMgPoint: North lane has pressure and an empty MG socket.
HoldFightingLine: center front is under pressure and friendly density is low.
```

Bad examples:

```text
Assigned because AI said so.
Mission score 77.
Unknown.
```

---

## Phase 1 implementation recommendation

Start with player mission labels only:

1. Add mission catalog entries for the four live templates.
2. Assign mission on spawn.
3. Store mission on `WarTeam` or command state sidecar.
4. Log assignment reason.
5. Display selected-squad mission in debug UI.
6. Do not yet force member tasks or replace `ChooseDecisionCore(...)`.
<!-- END FILE: 04_player_general_mission_assignment.md -->

<!-- BEGIN FILE: 05_enemy_general_spawn_tasking_difficulty.md -->
# 05 — Enemy General Spawn, Tasking, and Difficulty

## Purpose

The Enemy General should behave like a readable RTS skirmish opponent:

- no factory
- virtual supply/pressure budget
- difficulty tuning
- response delay
- lane choice
- counter-pick logic
- mission assignment
- fair information rules
- team caps
- escalation over time

It should replace or expand the current first-slice enemy response prototype in `TrenchworksSimulation`.

---

## Design principles

The enemy is allowed to be smart, not magical. It can use lane pressure, recent contact memory, approximate player pressure, virtual budget, difficulty profile, pressure debt, and comeback reserve. It should not create a feeling of instant perfect counters, unlimited hidden resources, perfect low/normal hidden knowledge, unexplained spawn positions, ignored caps, or ignored supply pressure.

Every enemy spawn should have a debug reason:

```text
Enemy Assault spawned in Center: pressure high, budget available, response delay complete.
Enemy Supply held back: team cap reached.
Enemy Engineer spawned in North: line needs hardpoint and comeback reserve released.
```

---

## Enemy General ownership

Owns virtual supply budget, pressure budget/debt, spawn cadence, response queue, team cap, difficulty profile, lane scoring, team-kind selection, enemy mission assignment, enemy support request prioritization, and escalation over time.

Does not own physical factory, player-side production, final combat outcomes, hidden player UI changes, or rendering.

---

## Virtual supply / pressure model

### `EnemyVirtualBudget`

Use a simple budget:

```text
currentBudget
pressureDebt
comebackReserve
lastIncomeTick
lastSpawnTick
nextAllowedSpawnTick
```

Budget rises over simulation time:

```text
currentBudget += profile.BudgetIncomePerMinute * elapsedMinutes
currentBudget = min(currentBudget, profile.MaxBudget)
```

### Pressure debt

Events that add pressure debt:

- player squad spawned
- player front establishment progress increases
- player holds a key hardpoint
- enemy front lane is pushed
- enemy squad destroyed or routed
- player contact consolidates

Pressure debt should not instantly spawn enemies. It should influence scoring and unlock budget/comeback reserve after delay.

### Comeback reserve

Comeback reserve helps prevent a dead match when the enemy falls behind. It releases after delay, cannot exceed team cap, should prefer stabilizing missions, and should be visible in debug. It should not spawn perfect counters on low/normal.

### Snowball throttle

If enemy is already ahead, reduce budget income, increase spawn cooldown, reduce aggression, and avoid overstacking the winning lane.

---

## Spawn cadence

Enemy can spawn only if all are true:

```text
simTick >= budget.NextAllowedSpawnTick
activeEnemyTeams < profile.HardTeamCap
currentBudget >= cheapestValidSpawnCost
responseDelaySatisfied
spawnLaneExists
```

Soft cap adds score penalty. Hard cap blocks spawn. Response delay means a player pressure event at tick `T` cannot be used until `T + profile response delay`.

---

## Difficulty profiles

### Recommended starting values

These are planning values. Codex should tune them after observing tick rate and match pacing.

| Knob | Recruit / Easy | Regular / Normal | Veteran / Hard | Brutal |
|---|---:|---:|---:|---:|
| Starting budget | 20 | 30 | 40 | 55 |
| Budget income | low | medium | high | very high |
| Max budget | 60 | 85 | 110 | 140 |
| Spawn cooldown | long | normal | short | very short |
| Response delay | long | normal | short | short |
| Soft team cap | 3-4 | 5-6 | 7-8 | 9-10 |
| Hard team cap | 5 | 7 | 9 | 12 |
| Aggression weight | 0.65 | 1.0 | 1.25 | 1.55 |
| Defense weight | 1.15 | 1.0 | 1.0 | 0.9 |
| Support weight | 0.75 | 1.0 | 1.1 | 1.2 |
| Counter-pick weight | 0.45 | 0.75 | 1.0 | 1.25 |
| Comeback multiplier | 0.5 | 0.8 | 1.0 | 1.2 |
| Supply generosity | low | normal | high | very high |
| Tech advance | slow | normal | fast | fastest |
| Info access | Visible only | Recent contact memory | Pressure approximation | Weighted omniscience-lite |
| Information noise | high | medium | low | low |

### Concrete profile example

```text
Recruit:
  StartingBudget = 20
  BudgetIncomePerMinute = 8
  MaxBudget = 60
  SpawnCooldownTicks = 180
  MinResponseDelayTicks = 120
  MaxResponseDelayTicks = 240
  SoftTeamCap = 4
  HardTeamCap = 5
  AggressionWeight = 0.65
  DefenseWeight = 1.15
  CounterPickWeight = 0.45
  InfoAccess = VisibleOnly

Regular:
  StartingBudget = 30
  BudgetIncomePerMinute = 12
  MaxBudget = 85
  SpawnCooldownTicks = 130
  MinResponseDelayTicks = 80
  MaxResponseDelayTicks = 160
  SoftTeamCap = 6
  HardTeamCap = 7
  AggressionWeight = 1.0
  DefenseWeight = 1.0
  CounterPickWeight = 0.75
  InfoAccess = RecentContactMemory

Veteran:
  StartingBudget = 40
  BudgetIncomePerMinute = 16
  MaxBudget = 110
  SpawnCooldownTicks = 95
  MinResponseDelayTicks = 50
  MaxResponseDelayTicks = 110
  SoftTeamCap = 8
  HardTeamCap = 9
  AggressionWeight = 1.25
  DefenseWeight = 1.0
  CounterPickWeight = 1.0
  InfoAccess = PressureApproximation

Brutal:
  StartingBudget = 55
  BudgetIncomePerMinute = 22
  MaxBudget = 140
  SpawnCooldownTicks = 70
  MinResponseDelayTicks = 30
  MaxResponseDelayTicks = 80
  SoftTeamCap = 10
  HardTeamCap = 12
  AggressionWeight = 1.55
  DefenseWeight = 0.9
  CounterPickWeight = 1.25
  InfoAccess = WeightedOmniscienceLite
```

---

## Fair information rules

| Difficulty | Allowed to know | Not allowed to know |
|---|---|---|
| Recruit | visible player contacts, enemy-owned front state, own squads, delayed direct pressure events | hidden support requests, exact hidden supply, unseen lane changes, perfect counter-picks |
| Regular | visible contacts, recent contact memory, approximate fighting pressure, own support needs, delayed player spawn lane | exact hidden composition, future plans, hidden resource counts |
| Veteran | approximate player pressure by lane, stale last-known team kinds, support pressure affecting visible front behavior | perfect real-time hidden positions, exact fogged support targets |
| Brutal | weighted omniscience-lite pressure map with noise, faster pressure interpretation, better counter-picks | UI/minimap leaks, spawning without budget, ignoring caps, exact perfect hidden info without noise |

---

## Enemy lane choice

| Input | Effect |
|---|---|
| Player pressure in lane | Increases response spawn score. |
| Enemy weak front | Increases defensive spawn score. |
| Enemy successful pressure | May reduce spawn score due to snowball throttle. |
| Open hardpoint need | Engineers/MG/support more likely. |
| Contact state | Confirmed contact enables assault/hold; suspected favors scout. |
| Lane overstacking | Penalty. |
| Recent player spawn lane | Bonus after response delay. |
| Comeback need | Bonus to losing lane, capped. |
| Safe spawn zone | Required. |

Pseudocode:

```csharp
float ScoreEnemyLane(LaneSnapshot lane, EnemyDifficultyProfile profile)
{
    float score = 0;
    score += lane.PlayerPressureEstimate * profile.AggressionWeight;
    score += lane.EnemyWeakness * profile.DefenseWeight;
    score += lane.OpenEnemySupportNeeds * profile.SupportWeight;
    score += lane.RecentPlayerSpawnPressure * profile.CounterPickWeight;

    if (lane.EnemyDensity > lane.DesiredEnemyDensity)
        score -= 25;

    if (!lane.HasValidEnemySpawnZone)
        return -9999;

    score += StableSmallTieBreaker(lane.Id);
    return score;
}
```

---

## Enemy team-kind selection

Early stage should use Scout, Assault, FortifyEngineer, and Supply. Mid stage can add MachineGun, Aid, Mortar, and Command. Late/special stage can add occult/ward or breach/pressure roles. For Phase 1, stay with existing supported templates unless the project already supports more.

| Player pressure | Enemy response candidates |
|---|---|
| Player scouts probing | Enemy scout screen or hold line. |
| Player assault pressure | Enemy assault hold, MG if unlocked, supply if line starving. |
| Player engineers building | Enemy assault pressure or scout mark; not instant perfect artillery. |
| Player supply chain | Enemy scout/pressure if visible; otherwise no direct hidden counter on low/normal. |
| Player MG/mortar future | Enemy scout mark, mortar counter-support, assault flank only if info allows. |
| Player casualty recovery | Enemy pressure only if visible and difficulty allows pressure estimate. |

Pseudocode:

```csharp
EnemySpawnCandidate SelectEnemySpawn(EnemyContext ctx)
{
    var lane = PickBestLane(ctx);
    var candidates = BuildTeamCandidates(lane, ctx);

    foreach (var candidate in candidates)
    {
        if (candidate.Cost > ctx.Budget.CurrentBudget)
            continue;
        if (!IsTeamAllowedByTechStage(candidate.TeamKind, ctx))
            continue;
        if (!IsTeamAllowedByCap(candidate.TeamKind, ctx))
            continue;

        candidate.Score += ScoreTeamNeed(candidate, lane, ctx);
        candidate.Score += ScoreCounterPick(candidate, lane, ctx);
        candidate.Score -= OverusePenalty(candidate.TeamKind, ctx);
    }

    return PickStableHighest(candidates);
}
```

---

## Enemy mission assignment

Enemy squads use the same mission catalog where possible.

| Enemy team kind | Likely missions |
|---|---|
| Scout | `ScoutProbe`, `MarkContact`, `ScreenFlank` |
| Assault | `HoldFightingLine`, `AssaultLine`, `RegroupWithdraw` |
| Engineer | `DigIn`, `ImproveTrench`, `BuildConnectTrench`, `ClaimBuildMgPoint` |
| Supply | `SupplyResupply`, `ReserveHold` |
| MachineGun future | `OccupyRifleBay`, `HoldFightingLine`, MG socket occupy |
| Mortar future | `MortarSupport`, `ReserveHold` |
| Aid future | `CasualtyResponse`, `ReserveHold` |
| Command future | `CommandRelay`, `ReserveHold` |

---

## Spawn selection end-to-end pseudocode

```csharp
void TickEnemyGeneral(int simTick)
{
    budget.UpdateIncome(simTick, profile);
    UpdatePressureMemory(simTick);

    if (simTick < budget.NextAllowedSpawnTick)
        return;

    if (ActiveEnemyTeams >= profile.HardTeamCap)
    {
        LogSpawnBlocked("HardTeamCap");
        return;
    }

    var ctx = BuildEnemyContext(simTick, profile);
    var candidate = SelectEnemySpawn(ctx);

    if (candidate == null)
    {
        LogSpawnBlocked("NoValidCandidate");
        return;
    }

    if (candidate.Cost > budget.CurrentBudget)
    {
        LogSpawnBlocked("InsufficientBudget");
        return;
    }

    var team = SpawnEnemyTeam(candidate);
    budget.CurrentBudget -= candidate.Cost;
    budget.LastSpawnTick = simTick;
    budget.NextAllowedSpawnTick = simTick + profile.SpawnCooldownTicks;

    var mission = AssignEnemyMission(team, candidate);
    CommandLog.EnemySpawned(team, mission, candidate.Reason);
}
```

---

## Enemy spawn costs

| Team kind | Cost | Notes |
|---|---:|---|
| Scout | 10 | Cheap pressure/visibility. |
| Assault | 18 | Main front pressure. |
| FortifyEngineer | 20 | Builds enemy durability. |
| Supply | 14 | Sustains enemy front. |
| Aid | 16 | Future. |
| MachineGun | 28 | Future, requires support/supply. |
| Mortar | 32 | Future, requires support request/spotter. |
| Command | 24 | Future, improves coordination. |

---

## Comeback and anti-snowball rules

Comeback is allowed if enemy front lost ground, active enemy teams are low, player front is strongly established, or enemy budget has been low for too long. It may increase budget income temporarily, lower spawn cooldown slightly, and prefer stabilizing missions. It must not exceed hard cap, ignore response delay entirely, spawn impossible positions, use hidden perfect low/normal info, or unlock expensive future tech too early.

If enemy is ahead, reduce budget income, increase cooldown, favor hold/support over new pressure, lower lane score where enemy density is high, and stop spawning at hard cap.

---

## Team cap handling

Soft cap penalty:

```text
spawnScore -= (activeEnemyTeams - softCap) * 12
```

Hard cap:

```text
no spawn
log EnemySpawnBlocked reason=HardTeamCap
```

Optional per-kind caps later: Scout 2, Assault 4, Engineer 2, Supply 2, MG 2, Mortar 1, Command 1.

---

## Debug examples

```text
EnemyGeneral: SpawnQueued Assault lane=Center delay=96 reason=PlayerPressure+WeakEnemyFront
EnemyGeneral: SpawnBlocked reason=InsufficientBudget budget=8 needed=18
EnemyGeneral: SpawnBlocked reason=HardTeamCap active=7 cap=7
EnemyGeneral: BudgetChanged +12 reason=Income elapsed=60s
EnemyGeneral: ComebackReserveReleased +10 reason=EnemyFrontLostGround
EnemyGeneral: MissionAssigned team=Enemy#22 mission=HoldFightingLine reason=CenterWeakFront+ConfirmedContact
```

---

## Phase 1 enemy implementation recommendation

First active enemy gate:

1. Create `EnemyDifficultyProfile` catalog with Recruit/Regular/Veteran/Brutal.
2. Add virtual budget and spawn cooldown.
3. Spawn only from existing supported templates.
4. Assign enemy mission from same bounded mission catalog.
5. Log spawn reason and blocked-spawn reason.
6. Disable or wrap old delayed response prototype behind `EnemyGeneral`.

Acceptance:

- Enemy spawn rate changes by difficulty.
- Enemy cannot exceed hard cap.
- Spawn reasons are visible in debug.
- No instant one-for-one direct response unless budget/delay/cap permits it.
<!-- END FILE: 05_enemy_general_spawn_tasking_difficulty.md -->

<!-- BEGIN FILE: 06_squad_mission_catalog.md -->
# 06 — Squad Mission Catalog

## Purpose

The mission catalog bounds the command system. Every general assignment should map to a known mission. Every mission should map to a limited set of likely `TeamDecisionKind` outputs.

The goal is not free-form behavior. The goal is readable, deterministic mission execution.

---

## Catalog rules

Every mission needs:

- mission id
- allowed team kinds
- intended front depth
- required/desired hardpoint family
- prerequisites
- success condition
- failure condition
- retask triggers
- likely `TeamDecisionKind` outputs

Recommended ID format:

```text
mission.scout.probe
mission.scout.mark_contact
mission.assault.line
mission.line.hold_fighting
mission.hardpoint.occupy_rifle_bay
mission.engineer.dig_in
mission.engineer.improve_trench
mission.engineer.build_connect_trench
mission.hardpoint.claim_build_mg_point
mission.supply.resupply
mission.medical.casualty_response
mission.support.mortar
mission.command.relay
mission.regroup.withdraw
mission.reserve.hold
```

---

## Front depth vocabulary

| Depth | Meaning |
|---|---|
| Front | Active fighting/contact line. |
| Support | Behind or adjacent to front; supports squads/hardpoints. |
| Rear | Safer logistics or command area. |
| Any | Mission may choose best valid depth. |

---

## Hardpoint family vocabulary

Use existing families from the project prompt: rifle/firing bay, front-line empty MG point, mortar pit, aid/doctor point, supply cache/depot, observation/signals, obstacle/wire/mines, engineering workshop/dugout, command dugout, sanitation/sustainment, occult/ward support, and breach/pressure socket.

Phase 1 should focus on rifle/firing bay, front-line empty MG point, supply cache/depot, observation/signals, and engineering workshop/dugout. Mortar, aid, command, occult/ward, and breach/pressure should stay future until the base mission/task loop is stable.

---

## Bounded mission catalog table

| Mission ID | Mission type | Allowed team kinds | Intended depth | Hardpoint family | Prerequisites | Success condition | Failure condition | Retask triggers | Likely `TeamDecisionKind` outputs |
|---|---|---|---|---|---|---|---|---|---|
| `mission.scout.probe` | `ScoutProbe` | Scout, Command future limited | Front/Support | observation/signals desired | safe path or acceptable risk; lane needs visibility | lane contact becomes `Suspected`/`Confirmed`, or scout reaches probe target | no safe path, pinned too long, severe casualties | confirmed heavy contact, no path, probe complete, lane overstacked | Scout, Occupy, Hold, MarkUnresolved, Withdraw, Regroup |
| `mission.scout.mark_contact` | `MarkContact` | Scout, Command, Mortar spotter future | Front/Support | observation/signals desired | suspected/confirmed contact exists | contact marked/held long enough for other squads/support | contact lost, scout suppressed, no safe path | contact consolidated, support request created, scout low supply | Scout, Hold, RequestSupport, MarkUnresolved, Withdraw |
| `mission.scout.screen_flank` | `ScreenFlank` | Scout, Assault limited | Front/Support | none; observation helpful | adjacent lane has pressure or unresolved contact | flank lane contact heat reduced or marked | flank contact overwhelms squad; no path | adjacent pressure changes, scout needed elsewhere | Scout, Hold, MarkUnresolved, Withdraw, Regroup |
| `mission.assault.line` | `AssaultLine` | Assault, MachineGun limited support | Front | rifle/firing bay desired | confirmed/suspected pressure; enough cohesion/supply | target line contested/held/consolidated | casualties high, out of ammo, no safe path, pinned too long | contact escalates, support request needed, front objective reached | Attack, Suppress, Bound, Flank, Assault, RequestSupport, Withdraw, Regroup |
| `mission.line.hold_fighting` | `HoldFightingLine` | Assault, MachineGun, Command limited, Scout emergency | Front | rifle/firing bay desired; MG desired | front sector needs defender; position exists or can be occupied | hold duration satisfied; contact held/consolidated | line collapses, no ammo, severe casualties | relieved, low ammo, new attack mission | Occupy, Hold, Suppress, RequestSupport, TreatCasualty, Withdraw, Regroup |
| `mission.hardpoint.occupy_rifle_bay` | `OccupyRifleBay` | Assault, MachineGun, Scout limited, Command limited | Front | rifle/firing bay required/desirable | built or claimable rifle/firing bay exists | squad occupies bay and holds through contact window | socket invalid, overrun, no safe path | bay completed and held, support needed, MG point available | Occupy, Hold, Suppress, RequestSupport, Withdraw |
| `mission.engineer.dig_in` | `DigIn` | FortifyEngineer, Assault emergency | Front/Support | engineering workshop desired | target position lacks cover; safe enough to work | trench/cover reaches minimum progress | contact too heavy, no safe path, build claim lost | cover complete, attack pressure, better build task | DigIn, Hold, RequestSupport, Withdraw, Regroup, Stall |
| `mission.engineer.improve_trench` | `ImproveTrench` | FortifyEngineer | Front/Support | engineering workshop desired | existing trench below desired depth/quality | trench improvement threshold reached | socket invalid, no supplies, contact too heavy | improvement complete, support request, MG build need | ImprovePosition, DigIn, Hold, RequestSupport, Stall |
| `mission.engineer.build_connect_trench` | `BuildConnectTrench` | FortifyEngineer | Support/Front | trench blueprint piece required | unconnected friendly positions; blueprint visible/claimable | connection completed or usable | no safe path, build blocked, duplicate claim | connection complete, contact escalation, supply shortage | ConnectTrenches, DigIn, ImprovePosition, Hold, RequestSupport, Stall |
| `mission.hardpoint.claim_build_mg_point` | `ClaimBuildMgPoint` | FortifyEngineer build; MachineGun occupy later | Front/Support | front-line empty MG point required | empty/started MG point; claim available; cover/support acceptable | MG point built or ready for crew | claim conflict, no supplies, contact too heavy | MG point complete, pressure changes, no path | BuildHardpoint, ImprovePosition, DigIn, Hold, RequestSupport, Stall |
| `mission.supply.resupply` | `SupplyResupply` | Supply, Porter-heavy future | Support/Front/Rear | supply cache/depot desired | ammo/supply request or low supply target; safe route | target resupplied above threshold | no safe path, target destroyed/withdrawn, supply depleted | request satisfied, higher request, team threatened | Resupply, Hold, RequestSupport, Withdraw, Regroup, Stall |
| `mission.medical.casualty_response` | `CasualtyResponse` | Aid; Assault emergency medic; Command limited | Support/Front | aid/doctor desired | wounded/casualty request; medical supplies | casualty treated/evacuated/stabilized | no safe path, medic down, target lost | request satisfied, team threatened, aid point full | TreatCasualty, Resupply, Hold, Withdraw, Regroup |
| `mission.support.mortar` | `MortarSupport` | Mortar, Command/Observer support | Rear/Support | mortar pit required/desirable | mortar team; support request/marked contact; ammo | support request serviced or contact disrupted in game terms | no ammo, no spotter/request, position threatened | request complete, ammo low, lane overrun | RequestSupport, Hold, Resupply, Withdraw, Regroup |
| `mission.command.relay` | `CommandRelay` | Command, Scout/Signaller limited | Support/Rear | command dugout or observation/signals desired | support chain weak, relay socket available | relay coverage active; support latency reduced | relay point invalid, command team threatened | front shifts, relay no longer needed, contact escalates | Hold, Occupy, RequestSupport, MarkUnresolved, Regroup |
| `mission.regroup.withdraw` | `RegroupWithdraw` | All | Any -> safer support/rear | regroup point desired | low cohesion, leader down, no safe path, pinned, low supply | squad reaches safe point and recovers threshold | no path, team destroyed, contact follows | recovered, new support route, emergency mission | Withdraw, Regroup, Hold, RequestSupport |
| `mission.reserve.hold` | `ReserveHold` | All | Support/Rear | depends on team kind | no higher-priority mission valid | team holds ready position; can accept retask | position threatened, support request appears, lane changes | new mission score higher, contact appears | Hold, Occupy, Resupply, TreatCasualty, Regroup |

---

## Required mission details

### `ScoutProbe`

Purpose: reveal or clarify lane state without committing heavy squads.

Allowed team kinds: Scout primary; Command future limited if signaller/observer composition exists.

Prerequisites: lane has low visibility or `ContactState.None/Suspected`, no existing scout probe claim in the same small sector, and a path exists or risk is acceptable.

Success: scout reaches probe target, contact state becomes `Suspected` or `Confirmed`, or lane is sufficiently observed for a time window.

Failure: no safe path, squad pinned beyond threshold, leader down with no fallback, casualties too high.

Likely outputs: `Scout`, `Occupy`, `Hold`, `MarkUnresolved`, `Withdraw`, `Regroup`.

### `MarkContact`

Purpose: turn suspected/confirmed contact into an actionable front/contact state. Allowed for Scout, Command with signaller/observer roles, and future spotting support. Success means contact remains marked/held through threshold and can be linked to support or assault/hold missions. Failure means contact lost, scout cannot observe, no safe observing position, or squad forced to withdraw.

### `AssaultLine`

Purpose: commit an assault/rifle team to pressure or contest a front line. Allowed for Assault primary; MachineGun only as support hold. Success means target line reaches held/consolidated state or squad occupies target fighting position. Failure means out of ammo, casualties too high, no safe path, pinned beyond recovery, or support request timeout.

### `HoldFightingLine`

Purpose: stabilize a lane/sector and prevent collapse. Allowed for Assault, MachineGun, Command limited, Scout emergency. Success means hold duration satisfied or contact held/consolidated. Failure means position overrun, ammo exhausted, no safe resupply, or severe casualties.

### `OccupyRifleBay`

Purpose: put a suitable squad in a rifle/firing bay. Allowed for Assault primary, MachineGun temporary, Scout observation, Command relay if safe. Success means squad occupies socket and bay remains held. Failure means socket invalid, claim conflict, heavy contact, or no safe path.

### `DigIn`, `ImproveTrench`, `BuildConnectTrench`

Purpose: create cover, improve trench quality, and connect positions. FortifyEngineer is primary. Success means trench/cover reaches threshold. Failure means invalid blueprint, duplicate claim, no supplies, no safe path, or contact too heavy.

### `ClaimBuildMgPoint`

Purpose: claim and build an MG point, or later assign MG crew to occupy one. Engineers build; MG crews occupy. Success means hardpoint built or crewed. Failure means claim denied, supply insufficient, support absent, or no safe path.

### `SupplyResupply`

Purpose: answer ammo/supply support requests and keep front squads useful. Success means target supply above threshold and support request closed. Failure means no safe route, target invalid, supply team depleted, or request already completed by another responder.

### `CasualtyResponse`

Purpose: answer medical pressure in a bounded, game-readable way. Aid teams are primary. Success means wounded stabilized, treated, or moved to aid point. Failure means no safe path, medic/doctor unavailable, target lost, or medical supplies depleted.

### `MortarSupport`

Purpose: let future mortar teams service fire-support requests through marked contacts and support chains. Success means support request serviced and ammo/cooldown updated. Failure means no ammo, no marked contact/spotter, mortar pit invalid, or team threatened.

### `CommandRelay`

Purpose: improve support routing, visibility, and command cohesion in a lane. Success means relay coverage active and selected lane has command coverage. Failure means relay socket invalid, team threatened, or no command/signals hardpoint.

### `RegroupWithdraw`

Purpose: every squad has a safe bounded fallback. Success means squad reaches regroup point and recovers threshold. Failure means no safe path, contact follows, or squad cannot move.

---

## Mission catalog implementation shape

Use static catalog entries at first:

```csharp
public sealed class MissionCatalogEntry
{
    public WarSquadMissionType Type;
    public string MissionId;
    public WarTeamKind[] AllowedTeamKinds;
    public FrontDepth IntendedDepth;
    public HardpointFamily RequiredOrDesiredHardpoint;
    public TeamDecisionKind[] LikelyDecisionOutputs;
    public string Notes;
}
```

Keep success/failure checks as named policy methods:

```text
MissionSuccessRules.IsScoutProbeComplete(...)
MissionFailureRules.IsMissionBlocked(...)
MissionRetaskRules.ShouldRetask(...)
```

Do not put all mission logic in one catalog object.

---

## Phase 1 mission scope

Implement active mission assignment for:

- `ScoutProbe`
- `MarkContact`
- `AssaultLine`
- `HoldFightingLine`
- `DigIn`
- `ImproveTrench`
- `BuildConnectTrench`
- `SupplyResupply`
- `RegroupWithdraw`
- `ReserveHold`

Keep these as future labels only until their teams exist:

- `ClaimBuildMgPoint`
- `MortarSupport`
- `CasualtyResponse`
- `CommandRelay`
- `OccupyRifleBay` if rifle bay sockets are not ready

---

## Pushback

The full catalog is useful, but Phase 1 should not attempt all missions at once. Start with the four live templates and the minimum fallback missions. Add MG/mortar/aid/command missions only after debug telemetry can clearly show why squads are assigned and retasked.
<!-- END FILE: 06_squad_mission_catalog.md -->

<!-- BEGIN FILE: 07_squad_leader_task_state_machines.md -->
# 07 — Squad Leader Task State Machines

## Purpose

The Squad Leader layer turns a `WarSquadMission` into squad-level task states and member-level task assignments.

It should answer:

```text
Given this mission, this squad composition, this contact state, this supply state, and this target:
what is the squad doing now, and what should each member try to do?
```

The Squad Leader does not choose strategic missions. The General does that.

---

## Squad leader ownership

Owns squad task state, local blackboard, mission progress, local support request decisions, leader-down fallback, member task assignment, and completion/failure reporting.

Reads `WarTeam`, `WarSubUnit`, `WarSquadMission`, front assignment/hardpoint target, contact state, supply/casualty state, current command claims, and recent `TeamDecisionKind` history.

Writes `SquadLeaderTaskState`, member tasks, support requests, mission status changes, and command log events.

---

## Local blackboard

Recommended fields:

```text
TeamId
ActiveMissionId
LeaderState
LocalContactState
LocalContactId
CurrentCoverSocketId
CurrentHardpointId
IsPinned
HasLowAmmo
HasCasualty
LeaderIsDown
HasSafePath
LastStateChangeTick
LastSupportRequestTick
LastMemberTaskAssignTick
StateReason
```

The blackboard should be rebuilt/updated from authoritative simulation state. It should not become a separate hidden truth.

---

## General state machine skeleton

```text
Mission Assigned
  |
  v
MovingToAssignment
  |
  +-- target reached --> mission-specific state
  |
  +-- contact in open --> OpenGroundContact
  |
  +-- no safe path --> Stalled or Regrouping
  |
  +-- leader down --> LeaderDownFallback
  |
  +-- low ammo/casualty --> Request support / regroup
```

Mission-specific states:

```text
OccupyingPosition
FightingFromPosition
BuildingTrench
ImprovingTrench
ClaimingHardpoint
Resupplying
MedicalResponse
Retreating
Regrouping
```

---

## State machine: moving to assignment

### State

```text
MovingToAssignment
```

### Entry conditions

- mission assigned
- target lane/sector/socket exists
- squad is not already at target

### Member tasks

| Role group | Task |
|---|---|
| Leader | `MoveToSquadTarget`, monitor cohesion |
| Scouts | `ObserveArc` while moving / `MarkContact` if triggered |
| Riflemen | `MoveToSquadTarget`, `HoldCover` on contact |
| Sappers/engineers | `MoveToSquadTarget`, reserve work task |
| Medics | `MoveToSquadTarget`, monitor wounded |
| Porters/supply | `CarrySupply`, follow squad |
| Signallers/observers | `RelayCommand` or `ObserveArc` if role exists |

### Transitions

| Condition | Next state |
|---|---|
| target reached | mission-specific state |
| contact confirmed in open | `OpenGroundContact` |
| pinned | `OpenGroundContact` or `Regrouping` |
| no safe path threshold | `Stalled` or `Regrouping` |
| leader down | `LeaderDownFallback` |
| mission cancelled/retasked | new mission state |

---

## State machine: occupying a position

Used by `HoldFightingLine`, `OccupyRifleBay`, `ScoutProbe` after reaching an observation point, `CommandRelay`, and `ReserveHold`.

| Role group | Task |
|---|---|
| Leader | assign sockets, watch support requests |
| Riflemen | `HoldCover`, `FireAtContact` if confirmed |
| Scouts | `ObserveArc`, `MarkContact` |
| MG gunner | `OperateMachineGun` if socket exists |
| Medics | `GuardMedic` or `TreatWounded` |
| Supply/porter | `CarrySupply`, `ResupplySquad` if needed |
| Signaller | `RelayCommand` |
| Engineer | `ImproveTrench` if mission permits, else `HoldCover` |

Transitions: confirmed contact -> `FightingFromPosition`; support needed -> stay and raise request; position held -> mission success or `ReserveHold`; socket invalid -> `Stalled`; critical low ammo/casualties -> support/regroup; leader down -> fallback.

---

## State machine: fighting from position

Used by `HoldFightingLine`, `AssaultLine` after reaching cover, `OccupyRifleBay`, and build missions under contact.

| Role group | Task |
|---|---|
| Leader | maintain hold, call support, manage withdrawal |
| Riflemen | `FireAtContact` or `SuppressContact` |
| Grenadier | support fire action if game supports it; otherwise `SuppressContact` |
| Trench marksman | `FireAtContact` from socket |
| MG gunner | `OperateMachineGun` |
| Scout | `MarkContact` / `ObserveArc` |
| Medic | `TreatWounded` when safe enough |
| Porter | `FetchAmmo` / `ResupplySquad` |
| Engineer | `RepairHardpoint` or `HoldCover` |

Transitions: contact held/consolidated -> occupying/success; pinned -> hold or regroup; low ammo -> request ammo then regroup if unresolved; casualties -> medical response; no safe path under pressure -> regroup.

---

## State machine: open-ground contact

Used when the squad is moving and contact occurs before assigned cover/socket.

| Role group | Task |
|---|---|
| Leader | choose cover/regroup/request support |
| Scouts | `MarkContact` if safe enough; otherwise `HoldCover` |
| Riflemen | `SuppressContact`, `HoldCover`, `BoundMove` |
| Engineers | `HoldCover`, avoid build tasks |
| Medics | `HoldCover`, treat only if safe |
| Porters | `HoldCover`, protect supply |
| Signallers | `RelayCommand`/support request if safe |

Transitions: cover reached -> `FightingFromPosition`; contact drops -> `MovingToAssignment`; pinned too long -> `Regrouping`; no safe path -> `Regrouping` or `Stalled`; casualties -> `MedicalResponse` or `Regrouping`.

Rule: do not let builders keep building in open-ground contact unless the mission explicitly says emergency dig-in and local state is safe enough.

---

## State machine: building / improving trench

States:

```text
BuildingTrench
ImprovingTrench
```

Used by `DigIn`, `ImproveTrench`, and `BuildConnectTrench`.

| Role group | Task |
|---|---|
| Leader | hold claim, assign workers/guards |
| Sapper | `DigTrench`, `BuildHardpoint`, `ClearObstacle` depending task |
| FieldEngineer | `DigTrench`, `ImproveTrench`, `BuildHardpoint`, `RepairHardpoint` |
| Riflemen | `GuardWorker`, `HoldCover` |
| Scout | `ObserveArc` |
| Medic | `GuardMedic` / treat if needed |
| Porter | `CarrySupply` / `FetchAmmo` / build supply handoff |
| Signaller | `RelayCommand` / support request if role exists |

Transitions: build threshold reached -> success/next build phase; contact confirmed -> `OpenGroundContact` or `FightingFromPosition`; worker supply low -> support request; claim lost -> `Stalled`; no safe path -> `Regrouping`; leader down -> fallback.

Guard-worker split:

```text
If squad has 4+ members:
  50-70% workers
  30-50% guards/observers
If contact suspected:
  reduce workers by one and increase guard/observe
If contact confirmed:
  pause work unless protected position exists
```

---

## State machine: claiming hardpoint

Used by `ClaimBuildMgPoint`, `OccupyRifleBay`, and future aid/supply/mortar/command socket missions.

Entry requires claim token, target hardpoint/socket, and compatible team kind/role.

| Role group | Task |
|---|---|
| Leader | maintain claim and socket assignment |
| Required operator | move to socket / operate / build depending hardpoint |
| Engineers | build/repair if hardpoint incomplete |
| Riflemen | guard |
| Scouts/observers | observe |
| Supply/porter | carry supply/ammo |
| Medic | hold/treat |

Transitions: hardpoint built by builder -> complete/hold; hardpoint occupied by crew -> fighting/occupying; claim denied -> stalled/retask; socket invalid -> failed; heavy contact -> fighting/regrouping.

---

## State machine: resupplying

Used by `SupplyResupply`.

| Role group | Task |
|---|---|
| QuartermasterRunner | choose route, manage delivery |
| Porter | `CarrySupply` |
| Rifleman/guard | `GuardWorker` / `HoldCover` |
| Medic if present | monitor/treat minor wounds only if safe |
| Leader | maintain support claim and request closure |

Transitions: target reached -> transfer supply; target supply above threshold -> complete; no safe path -> regroup/alternate route; target destroyed/withdrawn -> fail/retask; supply team threatened -> contact/regroup.

---

## State machine: medical response

Used by `CasualtyResponse` and local emergency within any squad.

| Role group | Task |
|---|---|
| CombatMedic | `TreatWounded` |
| FieldDoctor | `TreatWounded` at aid/doctor point |
| StretcherBearer | `CarryStretcher` |
| Riflemen | `GuardMedic` |
| Porter | carry medical supply if available |
| Leader | decide whether to stay, evacuate, or request aid |

Transitions: casualty stabilized -> previous mission/complete; area unsafe -> regroup/withdraw casualty; medical supplies low -> request supply; medic down -> request medical/regroup.

---

## State machine: retreat / regroup

Used by `RegroupWithdraw` and emergency fallback from any mission.

| Role group | Task |
|---|---|
| Leader/fallback leader | `RegroupOnLeader`, choose safe point |
| All mobile members | `WithdrawToSafePoint` |
| Riflemen/MG if able | suppress/hold briefly only as abstract cover behavior |
| Medic/stretcher | move wounded if safe enough |
| Porter | preserve supplies if possible; drop only if game supports emergency drop |

Transitions: regroup point reached -> complete/recovery; cohesion recovered -> retask; no safe path -> `Stalled`; contact follows -> fighting or continue withdrawal; leader down -> fallback.

---

## State machine: leader down fallback

Trigger: member with leader flag is down/unavailable.

Fallback priority:

```text
1. TrenchLieutenant
2. PatrolCorporal
3. Signaller
4. CombatMedic
5. Scout
6. Rifleman
7. FieldEngineer
8. QuartermasterRunner
9. Any healthy member by stable member ID
```

Immediate behavior:

```text
If contact active:
  assign temporary fallback leader
  set mission to Paused
  choose HoldCover / RegroupOnLeader
If no contact:
  assign fallback leader
  continue mission if safe
If no healthy fallback:
  mission fails -> RegroupWithdraw / support request
```

Transitions: fallback assigned and safe -> previous mission state; fallback assigned under heavy contact -> `Regrouping`; no fallback -> mission failed; original leader recovers -> optional return, avoid oscillation.

---

## Member completion/failure reporting

```text
MemberTaskController
  -> task completed/failed/interrupted
    -> SquadLeaderBrain updates blackboard
      -> SquadMissionController updates mission
        -> General may retask if needed
```

Bounded failure reasons:

```text
NoSafePath
TargetInvalid
ContactTooHeavy
LowAmmo
LowMedical
LeaderDown
ClaimDenied
SocketOccupied
SupportUnavailable
TaskExpired
MemberWounded
```

---

## Examples by squad

### Scout Patrol — `ScoutProbe`

```text
MovingToAssignment:
  PatrolCorporal -> MoveToSquadTarget
  Scout -> ObserveArc
  Rifleman -> HoldCover / MoveToSquadTarget

Target reached:
  PatrolCorporal -> HoldCover / manage contact
  Scout -> ObserveArc / MarkContact
  Rifleman -> GuardWorker or HoldCover

Contact suspected:
  Scout -> MarkContact
  PatrolCorporal -> RequestSupport if confirmed
  Rifleman -> HoldCover
```

### Assault Section — `HoldFightingLine`

```text
MovingToAssignment:
  Leader -> MoveToSquadTarget
  Riflemen -> MoveToSquadTarget
  Grenadier -> MoveToSquadTarget
  Medic -> follow, monitor wounded

Position reached:
  Riflemen -> HoldCover / FireAtContact
  Grenadier -> SuppressContact if contact
  Medic -> GuardMedic / TreatWounded
  Leader -> maintain hold and request support

Low ammo:
  Leader -> raise Ammo request
  Riflemen -> conserve / HoldCover
```

### Fortify Engineer Crew — `BuildConnectTrench`

```text
Moving:
  FieldEngineer/Sapper -> MoveToSquadTarget
  Rifleman/Scout -> ObserveArc / GuardWorker
  Porter -> CarrySupply

At blueprint:
  Sapper -> DigTrench
  FieldEngineer -> ImproveTrench / BuildHardpoint
  Rifleman -> GuardWorker
  Porter -> CarrySupply

Contact confirmed:
  Workers pause unless protected
  Guards hold
  Leader requests support or withdraws
```

### Supply Team — `SupplyResupply`

```text
Moving:
  QuartermasterRunner -> route lead
  Porters -> CarrySupply
  Rifleman/guard -> HoldCover
  Medic if present -> monitor

At target:
  Porters -> ResupplySquad
  QuartermasterRunner -> close support request
  Guard -> HoldCover

No safe path:
  pause, alternate route, or regroup
```

### Future MG Crew — `HoldFightingLine` / `OccupyRifleBay`

```text
Moving:
  MG gunner -> MoveToSocket
  Porter -> CarrySupply
  Rifleman -> GuardWorker
  Leader -> maintain socket claim

At MG point:
  MG gunner -> OperateMachineGun
  Porter -> FetchAmmo / ResupplySquad
  Rifleman -> HoldCover
  Scout/observer if present -> ObserveArc

Low ammo:
  Leader -> Ammo request
  MG gunner -> hold/suppress based on ammo
```

---

## Implementation guidance

Phase 1 should create leader state and assign high-level member tasks for debug, but should not force all member movement/combat behavior. First active tasks should be limited to `MoveToSquadTarget`, `HoldCover`, `ObserveArc`, `DigTrench`, `CarrySupply`, `ResupplySquad`, `TreatWounded`, and `RegroupOnLeader`.

Avoid deep per-member tactical behavior before mission assignment is visible, claims work, support requests are traceable, and Bob can see why squads do what they do.
<!-- END FILE: 07_squad_leader_task_state_machines.md -->

<!-- BEGIN FILE: 08_member_role_action_and_reaction_trees.md -->
# 08 — Member Role Action and Reaction Trees

## Purpose

Member behavior should be bounded, role-readable, and deterministic. Each member receives tasks from the `SquadLeaderBrain`, not directly from the General. Members react to local triggers using priority-ordered reaction trees.

This file defines the common action catalog, common reaction priority, role-specific action permissions, role-specific reactions, and trench/hardpoint socket interactions.

---

## Common action catalog

| Action / task | Meaning |
|---|---|
| `MoveToSquadTarget` | Move with squad toward assigned mission target. |
| `MoveToSocket` | Move to a trench/hardpoint/member socket. |
| `HoldCover` | Stay in or seek local cover; posture usually `Crouched`, `Prone`, or `DugIn`. |
| `ObserveArc` | Watch a lane/sector and update contact info. |
| `MarkContact` | Improve contact state from suspected/confirmed toward held/consolidated. |
| `FireAtContact` | Use normal combat behavior against confirmed contact. |
| `SuppressContact` | Abstract suppressive behavior; reduces contact pressure or pins in game terms. |
| `BoundMove` | Controlled movement under contact as an abstract team behavior. |
| `RegroupOnLeader` | Move/hold around leader or fallback leader. |
| `WithdrawToSafePoint` | Move toward assigned regroup point. |
| `DigTrench` | Work on trench/cover blueprint piece. |
| `ImproveTrench` | Improve existing trench quality/depth. |
| `BuildHardpoint` | Work on hardpoint socket. |
| `RepairHardpoint` | Restore damaged hardpoint. |
| `ClearObstacle` | Remove/clear obstacle if supported. |
| `PlaceObstacle` | Place wire/obstacle if supported. |
| `CarrySupply` | Carry ammo/food/material/medical stock in abstract inventory. |
| `ResupplySquad` | Transfer supply to target squad/hardpoint. |
| `FetchAmmo` | Move supply from cache/porter to operator/squad. |
| `TreatWounded` | Stabilize/treat wounded member. |
| `CarryStretcher` | Move wounded member toward aid point/regroup. |
| `OperateMachineGun` | Use MG hardpoint/socket if role and socket allow. |
| `OperateMortar` | Use mortar hardpoint/socket if role and socket allow. |
| `SpotForSupport` | Link marked contact to support request. |
| `RelayCommand` | Improve command/support chain from command/signals socket. |
| `GuardWorker` | Protect builders/supply/medical workers. |
| `GuardMedic` | Protect medic/doctor/stretcher task. |
| `IdleReserve` | Hold as local reserve. |

---

## Common deterministic reaction priority

When multiple triggers happen in the same tick, evaluate in this order:

| Priority | Trigger | Default response |
|---:|---|---|
| 1 | `Wounded` self | Interrupt task; seek hold/medical behavior. |
| 2 | `LeaderDown` | Pause mission; fallback leader logic; regroup if no fallback. |
| 3 | `RetreatOrdered` | Withdraw/regroup overrides normal task. |
| 4 | `SuppressionTaken` / pinned | Hold cover; report pinned. |
| 5 | `BeingAttacked` | Hold cover or fire/suppress if role allows. |
| 6 | `EnemySeen` confirmed | Report/mark/fire based on role and leader state. |
| 7 | `EnemyHeard` suspected | Report/observe; do not overcommit. |
| 8 | `LowAmmo` | Conserve/report/request resupply; operator may stop high-use action. |
| 9 | `LowMedical` / wounded teammate | Medic/doctor/stretcher respond if safe. |
| 10 | `NoSafePath` | Report blocked; hold/regroup. |
| 11 | `MissionTargetReached` | Switch to mission-specific task. |
| 12 | `HardpointSocketReached` / `TrenchSocketReached` | Begin socket task if claim valid. |
| 13 | `BuildTaskAssigned` | Begin work if safe enough. |
| 14 | `RegroupOrdered` | Move to leader/regroup point. |

Emergency triggers override normal work. Work tasks should not continue through heavy contact unless the state machine explicitly allows emergency dig-in.

---

## Role action and reaction catalog

### PatrolCorporal

| Category | Behavior |
|---|---|
| Core actions | `MoveToSquadTarget`, `RegroupOnLeader`, `HoldCover`, `ObserveArc`, `MarkContact`, limited `RelayCommand` |
| Support actions | `FireAtContact`, `SuppressContact`, `GuardWorker`, `GuardMedic` |
| Rare/forbidden | Rare: `DigTrench`, `CarrySupply`; Forbidden: `OperateMortar` unless catalog explicitly allows |
| Being attacked | Hold cover, keep squad cohesion, request support if contact confirmed. |
| Seeing/hearing enemy | Report contact, order observe/mark, avoid overcommitting alone. |
| Low ammo | Report; reduce aggressive tasks; request supply if acting leader. |
| Wounded teammate | Assign medic/guard; do not abandon leadership unless no medic and critical. |
| Leader down | High-priority fallback leader. |
| Socket interaction | Observation/rifle socket; coordinates trench/hardpoint claim but is not primary builder. |

### Scout

| Category | Behavior |
|---|---|
| Core actions | `ObserveArc`, `MarkContact`, `MoveToSquadTarget`, `MoveToSocket`, `HoldCover` |
| Support actions | `SpotForSupport`, `GuardWorker`, `FireAtContact` if confirmed and safe |
| Rare/forbidden | Rare: `BuildHardpoint`, `CarrySupply`; Forbidden: primary MG/mortar unless special template |
| Being attacked | Break observation if unsafe; hold cover; report contact. |
| Seeing/hearing enemy | Suspected -> observe; confirmed -> mark contact. |
| Low ammo | Continue observing; avoid fire tasks; report. |
| Wounded teammate | Report; guard medic if nearby; does not replace medic. |
| Leader down | Fallback after corporal/signaller depending priority. |
| Socket interaction | Observation/signals sockets; rifle bay limited; marks contacts from trench. |

### Rifleman

| Category | Behavior |
|---|---|
| Core actions | `HoldCover`, `FireAtContact`, `SuppressContact`, `MoveToSquadTarget`, `GuardWorker`, `GuardMedic` |
| Support actions | `BoundMove`, `RegroupOnLeader`, `WithdrawToSafePoint`, emergency `CarrySupply` |
| Rare/forbidden | Rare: `DigTrench`; Forbidden: primary medical/doctor/mortar/MG unless assigned role |
| Being attacked | Take cover, fire/suppress if confirmed contact and leader state allows. |
| Seeing/hearing enemy | Hearing -> report/hold; seeing -> fire or mark through squad if scout unavailable. |
| Low ammo | Switch to hold/conserve, raise ammo need. |
| Wounded teammate | Guard medic or help regroup; no advanced treatment. |
| Leader down | Possible fallback by stable ID after specialist leader roles. |
| Socket interaction | Rifle/firing bay primary; trench cover; guard hardpoint workers. |

### Sapper

| Category | Behavior |
|---|---|
| Core actions | `DigTrench`, `BuildHardpoint`, `ClearObstacle`, `PlaceObstacle`, `MoveToSocket` |
| Support actions | `ImproveTrench`, `RepairHardpoint`, `HoldCover`, `GuardWorker` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary medical/mortar unless special template |
| Being attacked | Pause work, hold cover, report build blocked. |
| Seeing/hearing enemy | Report; continue work only if contact suspected and guards cover. |
| Low ammo | Not primary shooter; report if unable to guard. |
| Wounded teammate | Stop work only if medic absent and casualty is nearby/critical. |
| Leader down | Low fallback priority unless engineer crew lacks leader. |
| Socket interaction | Trench build sockets, hardpoint build sockets, obstacle sockets. |

### CombatMedic

| Category | Behavior |
|---|---|
| Core actions | `TreatWounded`, `GuardMedic`, `MoveToSquadTarget`, `HoldCover` |
| Support actions | limited `CarryStretcher`, `RegroupOnLeader`, emergency report/relay |
| Rare/forbidden | Rare: `FireAtContact` self-defense; Forbidden: primary assault/build/mortar/MG |
| Being attacked | Hold cover; suspend treatment if unsafe; request guard. |
| Seeing/hearing enemy | Report; avoid initiating fire unless direct threat. |
| Low ammo | Usually not critical; report if self-defense unavailable. |
| Wounded teammate | Primary responder if safe enough. |
| Leader down | Fallback only if no command/corporal/scout option; prefers medical continuity. |
| Socket interaction | Aid/doctor point; trench cover; casualty/stretcher sockets. |

### QuartermasterRunner

| Category | Behavior |
|---|---|
| Core actions | `CarrySupply`, `ResupplySquad`, `FetchAmmo`, `MoveToSquadTarget` |
| Support actions | `RelayCommand`, `HoldCover`, `RegroupOnLeader` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary assault/medical/mortar/MG |
| Being attacked | Preserve supply if possible; hold/withdraw; report route unsafe. |
| Seeing/hearing enemy | Report route contact; avoid engagement. |
| Low ammo | Treat mission supply as critical; request source or return to cache. |
| Wounded teammate | Call medic; may carry supply to aid point. |
| Leader down | Low fallback unless supply team has no better role. |
| Socket interaction | Supply cache/depot sockets; supply handoff points; trench routes. |

### Porter

| Category | Behavior |
|---|---|
| Core actions | `CarrySupply`, `FetchAmmo`, `ResupplySquad`, `MoveToSquadTarget` |
| Support actions | `CarryStretcher`, limited `GuardWorker`, `HoldCover` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary assault command, mortar/MG operator unless special |
| Being attacked | Hold cover, preserve cargo, withdraw if ordered. |
| Seeing/hearing enemy | Report; avoid contact. |
| Low ammo | If carrying ammo, deliver; personal low ammo is report-only. |
| Wounded teammate | Can carry stretcher if assigned and route safe. |
| Leader down | Very low fallback priority. |
| Socket interaction | Supply cache/depot, aid carry points, trench route nodes. |

### FieldEngineer

| Category | Behavior |
|---|---|
| Core actions | `DigTrench`, `ImproveTrench`, `BuildHardpoint`, `RepairHardpoint`, `MoveToSocket` |
| Support actions | `ClearObstacle`, `PlaceObstacle`, `GuardWorker`, `HoldCover` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary medical/mortar/MG unless template says |
| Being attacked | Pause work; hold cover; request guard/support. |
| Seeing/hearing enemy | Suspected -> work if guarded; confirmed -> pause or cover. |
| Low ammo | Report; continue work if safe and guarded. |
| Wounded teammate | Report; may stop if no medic and casualty blocks job. |
| Leader down | Medium fallback in engineer squad. |
| Socket interaction | Engineering workshop/dugout, trench sockets, hardpoint build sockets. |

### MgGunner

| Category | Behavior |
|---|---|
| Core actions | `OperateMachineGun`, `SuppressContact`, `HoldCover`, `MoveToSocket` |
| Support actions | `FireAtContact`, ammo request through leader, `RegroupOnLeader` |
| Rare/forbidden | Rare: `CarrySupply`; Forbidden: primary build/medical/mortar unless special |
| Being attacked | Stay in socket if defensible; otherwise hold/withdraw by leader order. |
| Seeing/hearing enemy | Confirmed -> operate/suppress; suspected -> hold/observe unless scout marks. |
| Low ammo | Stop high-use suppression; request ammo; hold. |
| Wounded teammate | Continue role unless ordered; guard medic if no active contact. |
| Leader down | Not preferred fallback unless MG crew lacks corporal/assistant. |
| Socket interaction | MG point primary; rifle bay temporary; needs ammo support. |

### Grenadier

| Category | Behavior |
|---|---|
| Core actions | `SuppressContact`, `FireAtContact`, `HoldCover`, `BoundMove` |
| Support actions | `GuardWorker`, `RegroupOnLeader`, `WithdrawToSafePoint` |
| Rare/forbidden | Rare: `DigTrench`; Forbidden: primary medical/build/mortar/MG |
| Being attacked | Hold cover; support squad fire behavior. |
| Seeing/hearing enemy | Confirmed -> suppress/fire if leader allows; suspected -> report/hold. |
| Low ammo | Reduce special/high-cost actions; report. |
| Wounded teammate | Guard medic or cover withdrawal. |
| Leader down | Can fallback after corporal/scout/rifleman depending template. |
| Socket interaction | Rifle/firing bay and trench cover; no special hardpoint. |

### Signaller

| Category | Behavior |
|---|---|
| Core actions | `RelayCommand`, `SpotForSupport`, `ObserveArc`, `MoveToSocket` |
| Support actions | `MarkContact`, `HoldCover`, support request linkage |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary assault/build/medical/MG/mortar |
| Being attacked | Preserve relay; hold cover; report line threatened. |
| Seeing/hearing enemy | Report/mark; help support request linkage. |
| Low ammo | Not mission critical unless self-defense; report. |
| Wounded teammate | Call medical/support; guard if safe. |
| Leader down | High fallback after lieutenant/corporal. |
| Socket interaction | Observation/signals, command dugout, relay trench sockets. |

### ArtilleryObserver

| Category | Behavior |
|---|---|
| Core actions | `ObserveArc`, `MarkContact`, `SpotForSupport`, `RelayCommand` |
| Support actions | `HoldCover`, `MoveToSocket`, support request |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary build/medical/MG |
| Being attacked | Break spotting if unsafe; hold/withdraw; report. |
| Seeing/hearing enemy | Primary support-link role; mark confirmed contact. |
| Low ammo | Not mission critical; continue observation if safe. |
| Wounded teammate | Call medic; do not abandon observation unless urgent. |
| Leader down | Medium-high fallback for support teams. |
| Socket interaction | Observation/signals hardpoint, command relay, support spotting socket. |

### TrenchMarksman

| Category | Behavior |
|---|---|
| Core actions | `FireAtContact`, `ObserveArc`, `HoldCover`, `MoveToSocket` |
| Support actions | limited `MarkContact`, `GuardWorker`, limited `SuppressContact` |
| Rare/forbidden | Rare: `CarrySupply`; Forbidden: primary build/medical/mortar/MG |
| Being attacked | Hold cover; engage confirmed contact if safe. |
| Seeing/hearing enemy | Seeing -> fire/mark depending state; hearing -> observe/report. |
| Low ammo | Conserve; continue observation. |
| Wounded teammate | Guard medic if no immediate contact. |
| Leader down | Possible fallback in rifle team. |
| Socket interaction | Rifle/firing bay, observation slit, trench cover. |

### WireCutter

| Category | Behavior |
|---|---|
| Core actions | `ClearObstacle`, `MoveToSocket`, `HoldCover` |
| Support actions | `GuardWorker`, limited `DigTrench`, `RegroupOnLeader` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary medical/MG/mortar |
| Being attacked | Pause obstacle work; hold cover. |
| Seeing/hearing enemy | Report; do not continue exposed work under confirmed contact. |
| Low ammo | Report; not primary shooter. |
| Wounded teammate | Call medic; may help carry if safe. |
| Leader down | Low fallback priority. |
| Socket interaction | Obstacle/wire/mines family sockets; trench edges. |

### WireLayer

| Category | Behavior |
|---|---|
| Core actions | `PlaceObstacle`, `MoveToSocket`, `HoldCover`, limited `CarrySupply` |
| Support actions | limited `DigTrench`, `ImproveTrench`, `GuardWorker` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary medical/MG/mortar |
| Being attacked | Pause placement; hold/withdraw. |
| Seeing/hearing enemy | Report; continue only if safe/guarded. |
| Low ammo | Report; continue work if safe. |
| Wounded teammate | Call medic; help carry if assigned. |
| Leader down | Low fallback priority. |
| Socket interaction | Obstacle/wire family sockets; defensive trench edge sockets. |

### StretcherBearer

| Category | Behavior |
|---|---|
| Core actions | `CarryStretcher`, `MoveToSquadTarget`, `WithdrawToSafePoint`, `HoldCover` |
| Support actions | medical `CarrySupply`, `GuardMedic` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary assault/build/MG/mortar |
| Being attacked | Hold if carrying; seek cover; request guard. |
| Seeing/hearing enemy | Report; avoid exposed movement. |
| Low ammo | Not main concern; report. |
| Wounded teammate | Primary carry/evacuation responder if route safe. |
| Leader down | Very low fallback priority. |
| Socket interaction | Aid/doctor point, casualty sockets, regroup points. |

### FieldDoctor

| Category | Behavior |
|---|---|
| Core actions | `TreatWounded`, `MoveToSocket`, limited medical `RelayCommand`, `HoldCover` |
| Support actions | `GuardMedic`, medical stock resupply |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary assault/build/MG/mortar |
| Being attacked | Hold/withdraw; treatment pauses if unsafe. |
| Seeing/hearing enemy | Report; avoid combat. |
| Low ammo | Report only; medical supplies matter more. |
| Wounded teammate | Primary treatment at aid/doctor point. |
| Leader down | Not preferred fallback unless aid team lacks command role. |
| Socket interaction | Aid/doctor point primary; medical cache; casualty sockets. |

### TrenchMortarCrew

| Category | Behavior |
|---|---|
| Core actions | `OperateMortar`, `HoldCover`, `MoveToSocket`, limited self-ammo `ResupplySquad` |
| Support actions | `FetchAmmo`, `RegroupOnLeader`, limited `RelayCommand` |
| Rare/forbidden | Rare: `FireAtContact`; Forbidden: primary medical/build/MG |
| Being attacked | Stop mortar task if position threatened; hold/withdraw. |
| Seeing/hearing enemy | Does not self-select hidden targets; needs support request/marked contact. |
| Low ammo | Stop support action; request ammo. |
| Wounded teammate | Hold role unless ordered; call medic. |
| Leader down | Low fallback unless mortar team has no leader role. |
| Socket interaction | Mortar pit primary; supply cache nearby; support request link required. |

### TrenchLieutenant

| Category | Behavior |
|---|---|
| Core actions | `RelayCommand`, `RegroupOnLeader`, `MoveToSquadTarget`, `HoldCover`, support request management |
| Support actions | `ObserveArc`, limited `MarkContact`, `GuardWorker` |
| Rare/forbidden | Rare: direct build/supply carry; Forbidden: primary mortar/MG/medical unless special |
| Being attacked | Preserve command; choose hold/regroup/support request. |
| Seeing/hearing enemy | Coordinate contact report and support chain. |
| Low ammo | Request supply and reduce aggressive state. |
| Wounded teammate | Assign medic/stretcher/guard. |
| Leader down | Highest fallback if not already leader. |
| Socket interaction | Command dugout, observation/signals, relay sockets, rifle bay if emergency. |

---

## Special/future roles

Additional roles such as `PressureProjector`, `AetherLampScout`, `ClockworkTrenchhand`, `GraveSaltWarden`, `EchoRunner`, and `BoundShellCantor` should not receive unique behavior in Phase 1 unless they already have reliable gameplay systems. Map them temporarily to nearest safe action families.

| Role | Temporary family |
|---|---|
| AetherLampScout | Scout / observation |
| EchoRunner | Signaller / relay |
| ClockworkTrenchhand | FieldEngineer / porter |
| PressureProjector | MG/support pressure |
| GraveSaltWarden | Aid/ward support |
| BoundShellCantor | Mortar/support |

---

## Reaction tree templates

### Being attacked

```text
If self wounded:
  trigger Wounded
Else if current task is critical and cover socket exists:
  switch to HoldCover
Else if role can fight and contact confirmed:
  FireAtContact or SuppressContact
Else:
  HoldCover and report BeingAttacked
```

### Seeing enemy

```text
If role is Scout/Observer/Signaller:
  MarkContact or SpotForSupport
Else if role is combat role and leader state is FightingFromPosition:
  FireAtContact or SuppressContact
Else:
  Report contact and HoldCover
```

### Hearing enemy

```text
If scout/observer:
  ObserveArc toward suspected contact
Else:
  Report suspected contact
  Continue task only if not exposed
```

### Taking suppression

```text
Set posture Pinned or Prone as existing simulation allows
Interrupt exposed work
Report pinned
If pinned duration exceeds threshold:
  leader requests support or regroups
```

### Low ammo

```text
If role is MG/Mortar/Grenadier/Rifleman:
  reduce high-use actions
  request ammo through leader
If role is Supply/Porter:
  prioritize delivery if carrying ammo
Otherwise:
  report only
```

### Wounded teammate

```text
If CombatMedic/FieldDoctor and safe:
  TreatWounded
Else if StretcherBearer and assigned:
  CarryStretcher
Else if Rifleman/Guard:
  GuardMedic
Else:
  report casualty
```

### No safe path

```text
Stop movement task
Report NoSafePath
If mission is support delivery:
  ask leader for alternate route
If under contact:
  HoldCover / Regroup
Else:
  Stall until retask threshold
```

### Leader down

```text
Evaluate fallback leader priority
If fallback exists:
  assign fallback and pause current task briefly
  regroup on fallback leader
If no fallback:
  mission fails into RegroupWithdraw
```

### Mission target reached

```text
If socket/hardpoint task:
  validate claim and start socket task
If hold mission:
  occupy/hold
If scout mission:
  observe/mark
If supply/medical:
  deliver/treat
```

---

## Determinism rules

- Role reaction priority is fixed.
- Tie-breakers use stable member ID.
- A member can have one active task and one queued fallback task.
- A member does not receive tasks directly from General.
- Exposed work tasks are interrupted before combat/support reactions.
- Reaction outcomes write short reason strings.

---

## Phase 1 active role set

Start with:

- PatrolCorporal
- Scout
- Rifleman
- Sapper
- CombatMedic
- QuartermasterRunner
- Porter
- FieldEngineer

Keep MG/Mortar/Aid/Command roles in catalog but inactive until templates and hardpoints exist.

---

## Debug string examples

```text
Member Scout#2: ObserveArc -> MarkContact because EnemySeen.
Member Sapper#4: DigTrench interrupted because ContactConfirmed.
Member Porter#8: CarrySupply blocked because NoSafePath.
Member CombatMedic#5: TreatWounded assigned because Rifleman#3 wounded and area safe.
Member MgGunner#1: OperateMachineGun paused because LowAmmo.
```
<!-- END FILE: 08_member_role_action_and_reaction_trees.md -->

<!-- BEGIN FILE: 09_front_hardpoint_supply_contact_integration.md -->
# 09 — Front, Hardpoint, Supply, and Contact Integration

## Purpose

The command system must integrate with the existing front assignment, trench blueprint, hardpoint, support request, contact, visibility, and supply systems without replacing them.

The command layer should consume authoritative simulation state and write bounded intent:

```text
mission
task
claim
support request
debug event
```

It should not create a second hidden battlefield model.

---

## Integration map

| Existing/Planned system | Command layer use |
|---|---|
| `WarFrontAssignmentPlanner` | Finds valid front/support/rear/hardpoint targets and density. |
| `VisibleFrontBlueprintPieces` | Determines visible/eligible trench blueprint pieces for player-side work. |
| Trench blueprint pieces | Engineer missions and safe route improvements. |
| Hardpoint families | Mission target compatibility and member socket assignment. |
| Support requests | Supply, medical, fire support, engineer, regroup missions. |
| `ContactState` | Mission scoring, retask triggers, leader reactions. |
| Active/stalled sectors | Prioritize support/build/regroup. |
| Player visibility/scouting | Prevent hidden info leaks and guide scout value. |
| Supply inventory | Player-side support needs and squad sustainability. |
| Enemy virtual supply | Enemy spawn and sustainment abstraction. |

---

## Front assignment integration

`WarFrontAssignmentPlanner` already assigns squads to front/support/rear/hardpoint targets. The Player/Enemy General should not replace it. Instead:

```text
General builds mission candidate
  -> asks planner for valid assignment options
    -> scores options
      -> reserves claim if needed
        -> mission target references planner output
```

Data needed from planner:

| Data | Use |
|---|---|
| Candidate lane/sector targets | Mission target selection. |
| Front/support/rear depth | Mission depth matching. |
| Friendly/enemy density | Avoid overstacking. |
| Hardpoint targets | Build/occupy missions. |
| Stalled assignment reasons | Anti-stall support/build/regroup. |
| Existing claim/blueprint ownership | Avoid duplicate work. |

If the planner says no valid target exists, the command layer must assign fallback mission instead of inventing a target.

---

## `VisibleFrontBlueprintPieces` integration

Player-side build missions should only target blueprint pieces that are valid and visible/eligible for the player’s current information rules.

Use for:

- `DigIn`
- `ImproveTrench`
- `BuildConnectTrench`
- `ClaimBuildMgPoint`
- future supply/aid/command hardpoints

Do not allow Player General to assign build missions to hidden or invalid pieces unless the current game already permits it through the UI/simulation. Enemy General may use enemy-side virtual/known blueprint state according to difficulty and enemy ownership rules.

---

## Trench blueprint pieces

| Trench state | Mission effect |
|---|---|
| Missing connection | Boost `BuildConnectTrench`. |
| Shallow/weak trench | Boost `ImproveTrench`. |
| Front position exposed | Boost `DigIn`. |
| Completed safe route | Boost `SupplyResupply`, `CasualtyResponse`. |
| Blocked route | Boost engineer support or `RegroupWithdraw`. |

Engineer leader state should use blueprint task progress:

```text
BuildingTrench
ImprovingTrench
Stalled
Completed
```

Anti-chaos rule: one engineer crew owns a build claim per small trench piece unless the piece explicitly allows shared work slots.

---

## Hardpoint family integration

| Hardpoint family | Primary missions | Primary team/roles |
|---|---|---|
| rifle/firing bay | `OccupyRifleBay`, `HoldFightingLine` | Assault, Rifleman, TrenchMarksman |
| front-line empty MG point | `ClaimBuildMgPoint`, hold/suppress future | FortifyEngineer builds, MgGunner occupies |
| mortar pit | `MortarSupport` | Mortar, TrenchMortarCrew |
| aid/doctor point | `CasualtyResponse` | Aid, CombatMedic, FieldDoctor, StretcherBearer |
| supply cache/depot | `SupplyResupply`, `ReserveHold` | Supply, QuartermasterRunner, Porter |
| observation/signals | `ScoutProbe`, `MarkContact`, `CommandRelay` | Scout, Signaller, ArtilleryObserver |
| obstacle/wire/mines | future obstacle missions | WireCutter, WireLayer, Sapper |
| engineering workshop/dugout | engineer staging | FieldEngineer, Sapper |
| command dugout | `CommandRelay` | Command, TrenchLieutenant, Signaller |
| sanitation/sustainment | future sustainment | Supply/Aid future |
| occult/ward support | future special support | special roles only after stable |
| breach/pressure socket | future pressure/breach | special roles only after stable |

Hardpoint target rules:

- A mission can desire a hardpoint family without requiring it.
- If a mission requires a hardpoint and none exists, it should not be scored as valid.
- If a hardpoint is incomplete, distinguish build mission, occupy/crew mission, and defend workers mission.
- Claim must be valid before leader assigns socket tasks.

---

## Support request integration

Existing support request kinds:

```text
WarSupportRequestKind:
  Ammo
  Engineer
  FireSupport
  Medical
  Regroup
```

| Request kind | Mission response |
|---|---|
| Ammo | `SupplyResupply` |
| Engineer | `DigIn`, `ImproveTrench`, `BuildConnectTrench`, `ClaimBuildMgPoint` |
| FireSupport | `MortarSupport` future, `CommandRelay`/`MarkContact` support |
| Medical | `CasualtyResponse` |
| Regroup | `RegroupWithdraw`, `CommandRelay` support |

Support requests should be claimable:

```text
one primary responder
optional backup responder if request priority is Emergency
claim expires if responder cannot path or progress
```

Support request chain:

```text
Member reaction
  -> SquadLeaderBrain raises support request
    -> CommandEventLog records request
      -> General scores available support squads
        -> support squad assigned mission
          -> claim token created
            -> request closed/downgraded on success
```

---

## Contact integration

Contact states:

```text
None
Suspected
Confirmed
Held
Consolidated
```

| Contact state | Mission effect |
|---|---|
| None | Boost scout probe; avoid assault unless objective exists. |
| Suspected | Boost scout mark; moderate hold/occupy. |
| Confirmed | Boost assault/hold/MG/support; support teams avoid exposed routes. |
| Held | Boost consolidation, supply, improve trench. |
| Consolidated | Reduce scout/assault urgency; boost build/supply/command. |

Retask triggers:

- `None` -> `Suspected`: scout may continue or mark.
- `Suspected` -> `Confirmed`: assault/hold/support requests may appear.
- `Confirmed` -> `Held`: supply/build/occupy may become safer.
- `Held` -> `Consolidated`: mission complete or next phase.
- contact lost: scout/observer retask or `MarkUnresolved`.

---

## Visibility and minimap integration

Player-facing UI can show friendly mission/task state, visible/known contacts, support request chain, selected-squad reasons, and debug-only enemy info if debug mode is explicitly enabled.

Player UI should not show:

- hidden enemy spawn candidates
- hidden enemy budget in normal play
- hidden enemy target lane before it is revealed
- exact hidden enemy team kind/mission before contact

Debug overlay can show enemy internal state if Bob enables debug/dev view. Make it clear this is not normal player information.

---

## Supply integration

Player supply uses existing `WarTeam` supply state and support request memory.

| Supply state | Effect |
|---|---|
| Team low ammo | Boost `SupplyResupply`; reduce assault aggression. |
| Team out of ammo | Force hold/regroup/support request. |
| Engineer low material | Pause build or request supply. |
| Medical low | Aid team may need supply before casualty response. |
| Supply cache built | Boost nearby front sustainment. |

Enemy supply is represented by budget income, supply generosity, per-team supply values at spawn, difficulty-controlled resupply likelihood, and supply team spawns if needed. Enemy should still respect team caps, low ammo behavior, support requests, and mission failure if supply collapses.

---

## Reservation / claim rules

Without claims, multiple squads may choose the same hardpoint socket, build job, supply request, medical request, or front slot.

Claim lifecycle:

```text
ClaimRequested
  |
  +-- denied -> mission candidate penalty or failure
  |
  +-- granted
        |
        v
      Active
        |
        +-- renewed while progress occurs
        +-- released on success/failure/retask
        +-- expired after no progress
```

| Claim kind | TTL behavior |
|---|---|
| Mission target | medium TTL; renew while squad progresses. |
| Front assignment | short TTL; planner can refresh often. |
| Trench socket | medium TTL; expire if worker cannot path. |
| Hardpoint build job | long TTL; renew on build progress. |
| Hardpoint crew socket | medium/long while occupied. |
| Supply request | short/medium; expire if responder cannot path. |
| Medical request | short; emergency may reassign quickly. |
| Fire support request | short; cooldown-driven. |
| Regroup point | short/shared. |

Use sim ticks, not seconds.

Sharing rules:

| Target | Sharing |
|---|---|
| Small trench socket | exclusive |
| Hardpoint build job | exclusive unless hardpoint defines work slots |
| MG crew socket | exclusive |
| Rifle bay | slot-count based |
| Supply request | one primary + optional backup |
| Medical request | one primary + optional stretcher |
| Front lane | density capped, not exclusive |
| Regroup point | shared |

---

## Anti-chaos rules

- One active mission per squad.
- One emergency reaction state per squad.
- One active task and one fallback reaction per member.
- Retask only on defined triggers and cooldowns.
- Stable tie-breakers for target contention.
- Support teams should not all answer the same request.
- Engineers build; MG/assault/aid/supply/command teams occupy/use depending hardpoint family.

Stable target tie-breakers:

```text
1. higher mission priority
2. team kind better fit
3. older support request
4. closer/safe path
5. lower team ID
```

---

## Anti-stall rules

Mark a mission stalled if the same leader state persists too long without progress, no safe path repeats, claim invalid repeats, member tasks fail repeatedly, support request is unanswered after threshold, contact prevents work for threshold, or target becomes invalid.

| Stall reason | Response |
|---|---|
| NoSafePath | try alternate assignment or `RegroupWithdraw`. |
| ClaimDenied | choose next target. |
| ContactTooHeavy | request assault/support or pause build. |
| LowSupply | raise supply request or regroup. |
| NoWorker | retask mission or wait for correct team. |
| TargetInvalid | mission fail and retask. |
| SupportUnavailable | downgrade mission or regroup. |

Debug example:

```text
MissionStalled: Team 9 BuildConnectTrench blocked 90 ticks reason=NoSafePath target=TrenchPiece_N_04
```

---

## Integration with current decision history

`WarTeam` already stores recent decision history. Use it for detecting repeated `Stall`, repeated `Withdraw`/`Regroup`, retask decisions, mission failure, and confirming mission bias is working.

Example:

```text
If mission=SupplyResupply and last 5 decisions include Stall/NoSafePath,
then expire supply request claim and retask.
```

---

## Phase 1 integration plan

1. Read front/hardpoint/contact/supply snapshots.
2. Assign mission using existing planner outputs.
3. Add claim registry for support requests and hardpoint/build sockets.
4. Use decision history to detect stalls.
5. Show mission/claim/support chain in debug UI.
6. Only then activate deeper member tasks.

---

## Pushback

Do not build a second battlefield model inside `WarCommandDirector`. It should use snapshots of existing systems and write bounded command state. The existing simulation remains the source of truth.
<!-- END FILE: 09_front_hardpoint_supply_contact_integration.md -->

<!-- BEGIN FILE: 10_telemetry_debug_ui_and_playtest_tools.md -->
# 10 — Telemetry, Debug UI, and Playtest Tools

## Purpose

Bob needs to see why squads do what they do. The command/tasking system will look broken if mission assignment, retasking, support requests, claims, and enemy spawns are hidden.

Debugging should answer:

```text
Why did this squad get this mission?
Why did it retask?
Why did the enemy spawn that squad?
Why is this member not doing the job?
What claim or support request is blocking progress?
```

---

## Selected squad debug panel

When a squad is selected, show compact command info.

| Field | Example |
|---|---|
| Team ID / kind / faction | `Player Team 12 / FortifyEngineer` |
| Current `WarOrder` | `Fortify` |
| Current mission | `BuildConnectTrench` |
| Mission status | `Active` |
| Mission priority | `High` |
| Assignment reason | `SelectedLane+WeakTrenchDepth+NoClaimConflict` |
| Target lane/sector/socket | `North / N-Front-02 / TrenchPiece_N_04` |
| Claim token | `BuildJob#31 active, expires in 44 ticks` |
| Squad leader state | `BuildingTrench` |
| Last tactical phase | `Digging` |
| Contact state | `Suspected` |
| Supply state | `Ammo 62%, Materials 40%` |
| Support request | `None` or `Ammo#18 pending` |
| Retask lockout | `locked 36 ticks` |
| Last retask reason | `NoSafePath` |
| Recent command events | last 3-5 |

Compact example:

```text
Team 12 FortifyEngineer
Mission: BuildConnectTrench [Active / High]
Reason: SelectedLane + WeakTrenchDepth + NoClaimConflict
Leader: BuildingTrench
Target: North / TrenchPiece_N_04
Claim: BuildJob#31 active
Contact: Suspected
Supply: Material 40%
Recent: Worker assigned, Scout observing, no support request
```

---

## Member debug panel

For selected squad, show member rows.

| Member | Role | Task | Status | Reaction | Reason |
|---|---|---|---|---|---|
| #1 | PatrolCorporal | RegroupOnLeader | Assigned | None | leader |
| #2 | Sapper | DigTrench | Working | None | mission build task |
| #3 | FieldEngineer | ImproveTrench | Working | None | mission build task |
| #4 | Rifleman | GuardWorker | Waiting | EnemyHeard | suspected contact |
| #5 | Porter | CarrySupply | Moving | None | material delivery |

Keep this compact. Do not dump huge data.

---

## General assignment reason display

Player General:

```text
PlayerGeneral assigned ScoutProbe:
selected lane Center needs visibility; no scout claim exists.
```

Enemy General debug-only:

```text
EnemyGeneral spawned Assault:
Center pressure high; budget 42 >= cost 18; cooldown complete; team cap 4/7.
```

Do not show hidden enemy details in normal player UI.

---

## Enemy director debug panel

Debug-only panel for Bob/dev.

| Field | Example |
|---|---|
| Difficulty | `Regular` |
| Current budget | `42 / 85` |
| Income rate | `12/min` |
| Pressure debt | `18` |
| Comeback reserve | `6` |
| Next spawn allowed | `in 58 ticks` |
| Active teams | `4 / soft 6 / hard 7` |
| Last spawn | `Assault Center HoldFightingLine` |
| Last blocked spawn | `InsufficientBudget needed=28 budget=11` |
| Info access | `RecentContactMemory` |
| Aggression/defense/support weights | `1.0 / 1.0 / 1.0` |

Example:

```text
EnemyGeneral [Regular]
Budget: 42/85 (+12/min)
PressureDebt: 18
Cap: 4 active / 6 soft / 7 hard
NextSpawn: 58 ticks
LastSpawn: Assault Center -> HoldFightingLine
Reason: PlayerPressure+WeakEnemyFront
Info: RecentContactMemory
```

---

## Front/claims overlay

Overlay layers:

| Layer | What it shows |
|---|---|
| Mission targets | squad icons linked to lane/sector/socket. |
| Claim tokens | target sockets with owner team ID. |
| Support requests | ammo/medical/engineer/fire/regroup request markers. |
| Stalled sectors | warning icon and reason. |
| Contact state | known contact state only; hidden enemy data debug-only. |
| Hardpoint state | empty/started/completed/occupied. |

Claim tooltip:

```text
Claim BuildJob#31
Owner: Team 12 FortifyEngineer
Target: MG_N_02
Mission: ClaimBuildMgPoint
Expires: 44 ticks
Reason: EmptyMgPoint+FrontPressure
```

---

## Command event logging

Use stable event names:

```text
Command.PlayerSquadSpawned
Command.EnemySpawnQueued
Command.EnemySpawned
Command.EnemySpawnBlocked
Command.MissionCandidateScored
Command.MissionAssigned
Command.MissionRetasked
Command.MissionCompleted
Command.MissionFailed
Command.ClaimCreated
Command.ClaimDenied
Command.ClaimReleased
Command.ClaimExpired
Command.SquadLeaderStateChanged
Command.MemberTaskAssigned
Command.MemberTaskCompleted
Command.MemberTaskFailed
Command.SupportRequestRaised
Command.SupportRequestAccepted
Command.SupportRequestCancelled
Command.EnemyBudgetChanged
Command.DifficultyProfileApplied
```

Log shape:

```text
[tick] event team/member/mission target score reason
```

Examples:

```text
[01420] Command.MissionAssigned team=12 mission=BuildConnectTrench target=TrenchPiece_N_04 score=78.5 reason=SelectedLane+WeakTrenchDepth
[01424] Command.ClaimCreated team=12 claim=BuildJob#31 target=TrenchPiece_N_04 ttl=120
[01501] Command.MemberTaskFailed team=12 member=4 task=GuardWorker reason=NoSafePath
[01520] Command.MissionRetasked team=12 from=BuildConnectTrench to=RegroupWithdraw reason=NoSafePathThreshold
[01610] Command.EnemySpawnBlocked reason=HardTeamCap active=7 cap=7
```

---

## Good debug strings

```text
Assigned ScoutProbe because Center has low visibility, selected lane bonus, and no scout is already assigned.
Assigned SupplyResupply because Assault#8 requested ammo and the request is unclaimed.
Assigned HoldFightingLine because South front is under pressure and friendly density is low.
Retasked BuildConnectTrench -> RegroupWithdraw because no safe path for 90 ticks.
Retasked ScoutProbe -> MarkContact because contact changed from Suspected to Confirmed.
Enemy spawned FortifyEngineer because North enemy line is weak, budget is available, and cooldown is complete.
Enemy did not spawn because hard team cap reached.
Sapper#3 started DigTrench because mission BuildConnectTrench owns the trench claim.
CombatMedic#5 paused TreatWounded because contact became confirmed and no guard was assigned.
```

Bad strings:

```text
AI chose mission.
Score was best.
Task failed.
Enemy spawned.
```

---

## Playtest tools

### Command event inspector

A small scrollable event list with filters: faction, team ID, event kind, lane, support request kind, mission type.

### Selected lane inspector

Shows active friendly missions, active enemy missions in debug mode only, support requests, hardpoint/build claims, contact state, and stalled reason.

### Force debug actions

For dev builds only:

| Action | Use |
|---|---|
| Force player mission re-score | Test retasking. |
| Force enemy budget +10 | Test spawn selection. |
| Force support request | Test supply/medical assignment. |
| Force contact state | Test reaction trees. |
| Force claim expire | Test anti-chaos. |
| Toggle difficulty profile | Test enemy knobs. |

Do not expose these in normal player UI.

---

## Telemetry counters

| Counter | Meaning |
|---|---|
| Missions assigned per type | Check mission variety and overuse. |
| Retasks per minute | Detect thrashing. |
| Mission failures by reason | Find broken pathing/claims/supply. |
| Enemy spawns by type/difficulty | Tune difficulty. |
| Spawn blocks by reason | Find caps/budget issues. |
| Claims denied by kind | Find overcontention. |
| Support requests opened/closed | Measure support chain health. |
| Member task failures by reason | Find role/task bugs. |
| Average time stalled | Detect deadlocks. |

---

## Save/replay test visibility

For deterministic testing, add a command debug dump:

```text
CommandDebugDump tick=2000
  missions:
    team=1 ScoutProbe Active target=Center reason=...
  enemy:
    difficulty=Regular budget=42 nextSpawn=...
  claims:
    BuildJob#31 team=12 target=...
  recentEvents:
    ...
```

This dump can be compared between two runs with the same seed.

---

## UI implementation priority

| Gate | Debug/UI focus |
|---|---|
| Gate 1 | selected squad mission label, assignment reason, recent command events |
| Gate 2 | claim/support request fields, retask reason, mission status |
| Gate 3 | enemy debug panel, budget/cap/spawn reason |
| Gate 4 | member task rows, leader state, task failure reason |
| Gate 5 | overlay for claims/support/stalls |

---

## Acceptance criteria for debug usability

Bob should be able to select any squad and answer:

1. What mission is it on?
2. Why was it assigned?
3. What is the squad leader trying to do?
4. What is each member doing?
5. Is it blocked by contact, supply, path, claim, or target invalid?
6. Did the enemy spawn because of pressure, budget, comeback, or difficulty?
7. Is a support request claimed, unclaimed, completed, or stale?

If the answer is not visible, the system is not ready for deeper autonomy.
<!-- END FILE: 10_telemetry_debug_ui_and_playtest_tools.md -->

<!-- BEGIN FILE: 11_implementation_gates.md -->
# 11 — Implementation Gates

## Purpose

This command/tasking system is broad. It should not be implemented all at once.

Each gate below lists goal, likely files touched, data contracts added, code changes, tests/smokes, acceptance criteria, and rollback risks. Gate 1 is intentionally small enough for one Codex worker to implement safely.

---

## Gate 1 — Shadow command contracts and event log

### Goal

Add the minimal command data contracts and event log with no gameplay behavior change.

### Files likely touched

```text
Assets/Scripts/Simulation/War/WarTeamTypes.cs
Assets/Scripts/Simulation/War/WarTeamEntities.cs
Assets/Scripts/Simulation/War/Command/WarCommandTypes.cs       (new)
Assets/Scripts/Simulation/War/Command/CommandEventLog.cs       (new)
Assets/Scripts/Simulation/War/Command/WarCommandDirector.cs    (new stub)
Assets/Scripts/Simulation/TrenchworksSimulation.cs             (wire stub carefully)
```

If the project does not use subfolders, place new files under `Assets/Scripts/Simulation/War/` with clear `WarCommand...` names.

### Data contracts added

```text
WarSquadMissionType
WarMissionStatus
WarMissionPriority
WarGeneralIntent
EnemyDifficultyTier
WarSquadMission
AssignmentScoreBreakdown
CommandEventKind
CommandEventLogEntry
CommandEventLog
```

### Code changes

- Add command event log ring buffer.
- Add `WarCommandDirector` stub with `Initialize(...)`, `TickCommandLayer(...)`, and `OnWarTeamSpawned(...)`.
- Add a safe place to store current mission: either `WarTeam.ActiveMissionId` plus command director mission map, or a sidecar map keyed by team ID.
- Do not alter `WarTeamSlice.ChooseDecisionCore(...)`.
- Do not alter enemy spawn behavior yet except optional logging.

### Tests/smokes

- Project compiles.
- WAR tray still spawns current four player templates.
- Existing enemy response still works as before.
- Command event log receives spawn/debug event if hooked.
- No null references when command director is absent/disabled.

### Acceptance criteria

- Selecting or inspecting a team can show “No active mission” or placeholder mission state.
- Event log can record and prune entries.
- No behavior changes to squad movement/combat/front assignment.
- No change to factory/player-side production.

### Rollback risks

Low. Remove new command files and hook calls.

---

## Gate 2 — Player General mission assignment on spawn

### Goal

Assign a bounded mission to newly spawned player squads.

### Files likely touched

```text
Assets/Scripts/Simulation/War/Command/PlayerGeneral.cs          (new)
Assets/Scripts/Simulation/War/Command/CommandMissionCatalog.cs  (new)
Assets/Scripts/Simulation/War/Command/WarCommandDirector.cs
Assets/Scripts/Simulation/TrenchworksSimulation.cs
Assets/Scripts/Simulation/IntegratedPrototypeSystems.cs         (only if spawn return needs team ID)
Assets/Scripts/Unity/PrototypeBootstrap.cs                      (only if lane/doctrine info missing)
```

### Data contracts added

```text
MissionScoreContext
MissionCatalogEntry
```

### Code changes

- Create mission catalog entries for live templates: `ScoutProbe`, `MarkContact`, `AssaultLine`, `HoldFightingLine`, `DigIn`, `ImproveTrench`, `BuildConnectTrench`, `SupplyResupply`, `RegroupWithdraw`, `ReserveHold`.
- Add `PlayerGeneral.AssignMissionForNewSquad(...)`.
- Hook player spawn event after `IntegratedPrototypeSystems.SpawnWarTeam(...)`.
- Store mission and assignment reason.
- Log `Command.MissionAssigned`.

### Tests/smokes

- Spawn `scout_patrol`; verify scout/probe/mark mission.
- Spawn `assault_section`; verify assault/hold mission.
- Spawn `fortify_engineers`; verify dig/improve/connect mission.
- Spawn `supply_team`; verify supply/reserve mission.
- Spawn in different lanes; mission target lane respects selected lane when valid.
- No crash if no front target exists.

### Acceptance criteria

- Every player-spawned squad gets exactly one active mission or fallback.
- Assignment reason is readable.
- Existing team behavior still works.
- No member task execution required yet.

### Rollback risks

Medium-low. Disable `PlayerGeneral` hook; existing spawn flow remains.

---

## Gate 3 — Selected squad debug UI / overlay basics

### Goal

Make command state visible to Bob.

### Files likely touched

Exact UI files are not listed in the prompt, so Codex should locate current selected squad/HUD/debug UI files. Likely areas:

```text
Assets/Scripts/Unity/...
Assets/Scripts/Simulation/War/Command/CommandEventLog.cs
Assets/Scripts/Simulation/War/Command/WarCommandDirector.cs
```

### Data contracts added

None, unless a simple `CommandDebugViewModel` is needed.

### Code changes

- Add selected squad command panel fields: mission, status, target lane/sector/socket, assignment reason, current order, last tactical phase, recent command events.
- Add compact “No active mission” fallback display.
- Add event log formatting helpers.

### Tests/smokes

- Select each live team type.
- Confirm mission info is shown.
- Confirm no hidden enemy info appears in normal UI.
- Confirm UI handles destroyed/removed team safely.

### Acceptance criteria

- Bob can see mission and reason for a selected player squad.
- Debug strings are short and readable.
- UI does not decide mission/combat behavior.

### Rollback risks

Medium. UI changes can be disabled with debug flag.

---

## Gate 4 — SquadMissionController biases existing decisions

### Goal

Make missions gently influence existing `WarTeamSlice` decisions without replacing the local brain.

### Files likely touched

```text
Assets/Scripts/Simulation/War/WarTeamSlice.cs
Assets/Scripts/Simulation/War/Command/SquadMissionController.cs (new)
Assets/Scripts/Simulation/War/Command/CommandMissionCatalog.cs
Assets/Scripts/Simulation/War/Command/WarCommandDirector.cs
```

### Data contracts added

```text
MissionDecisionHint
MissionProgressState
```

### Code changes

- Add `SquadMissionController.GetDecisionHints(team, mission, snapshot)`.
- Mission hints return preferred `TeamDecisionKind` list, disallowed/penalized decisions, hold reason hints, and completion/failure checks.
- `WarTeamSlice.ChooseDecisionCore(...)` consumes hints as bias, not absolute command.
- Log mission completion/failure/blocked.

### Tests/smokes

- Scout mission favors `Scout`/`MarkUnresolved`/`Hold`.
- Engineer mission favors `DigIn`/`ImprovePosition`/`ConnectTrenches`.
- Supply mission favors `Resupply`.
- Assault mission favors `Attack`/`Suppress`/`Hold`.
- Local safety still overrides mission bias under emergency contact.

### Acceptance criteria

- Missions visibly change likely decisions in expected way.
- Emergency contact/low ammo/no path behavior still works.
- No giant monolithic method added.

### Rollback risks

Medium. Disable mission hints and return to existing decisions.

---

## Gate 5 — Claim/reservation registry

### Goal

Prevent multiple squads from choosing the same small hardpoint/build/support target.

### Files likely touched

```text
Assets/Scripts/Simulation/War/Command/CommandClaimRegistry.cs   (new)
Assets/Scripts/Simulation/War/Command/WarCommandTypes.cs
Assets/Scripts/Simulation/War/Command/PlayerGeneral.cs
Assets/Scripts/Simulation/War/Command/SquadMissionController.cs
Assets/Scripts/Simulation/War/WarFrontAssignment.cs
```

### Data contracts added

```text
CommandClaimKind
CommandClaimToken
```

### Code changes

- Add claim create/release/renew/expire.
- Start with hardpoint build job claims, trench socket claims, and supply request claims.
- Apply claim penalties in mission scoring.
- Release claims on mission complete/fail/retask.
- Expire claims with no progress.

### Tests/smokes

- Spawn two engineer teams; they should not claim same build socket unless sharing allowed.
- Spawn two supply teams; one primary responder per ammo request.
- Expired claim becomes available.
- Destroyed/invalid target releases claim.

### Acceptance criteria

- Claim conflicts are logged.
- Duplicate assignment chaos is reduced.
- Claim TTLs use sim ticks.

### Rollback risks

Medium. Claim bugs can block missions; add debug override to clear all claims.

---

## Gate 6 — Retasking policy

### Goal

Allow Player General to retask squads when bounded triggers occur.

### Files likely touched

```text
Assets/Scripts/Simulation/War/Command/PlayerGeneral.cs
Assets/Scripts/Simulation/War/Command/SquadMissionController.cs
Assets/Scripts/Simulation/War/Command/CommandMissionCatalog.cs
Assets/Scripts/Simulation/War/Command/CommandClaimRegistry.cs
```

### Data contracts added

```text
RetaskEvaluation
RetaskTriggerKind
```

### Code changes

- Add retask trigger checks: complete, no safe path, low ammo, leader down, target invalid, claim denied/expired, support request priority, contact escalation.
- Add retask cooldowns.
- Require replacement score margin.
- Release old claims and create new claims.

### Tests/smokes

- Scout retasks from probe to mark contact when contact confirmed.
- Engineer retasks if target build piece becomes invalid.
- Supply retasks when request completed.
- Assault requests/regroups when out of ammo.
- Retask does not thrash every tick.

### Acceptance criteria

- Retasks happen for obvious reasons.
- Retask reasons are logged.
- Cooldowns prevent chaos.

### Rollback risks

Medium-high. Retasking can destabilize behavior; include global debug toggle.

---

## Gate 7 — Enemy General virtual budget and difficulty

### Goal

Replace the direct delayed enemy-response prototype with budgeted, capped, difficulty-driven enemy spawning.

### Files likely touched

```text
Assets/Scripts/Simulation/TrenchworksSimulation.cs
Assets/Scripts/Simulation/War/Command/EnemyGeneral.cs           (new)
Assets/Scripts/Simulation/War/Command/EnemyDifficultyCatalog.cs (new)
Assets/Scripts/Simulation/War/Command/WarCommandDirector.cs
Assets/Scripts/Simulation/IntegratedPrototypeSystems.cs
```

### Data contracts added

```text
EnemyDifficultyProfile
EnemyVirtualBudget
EnemySpawnCandidate
EnemyInfoAccessLevel
```

### Code changes

- Add difficulty catalog.
- Add virtual budget income.
- Add spawn cooldown and response delay.
- Add team soft/hard cap.
- Add lane scoring.
- Spawn from current supported enemy templates.
- Assign enemy mission from mission catalog.
- Disable/wrap old delayed response logic.

### Tests/smokes

- Recruit spawns slower/fewer than Regular.
- Veteran/Brutal apply higher pressure but respect caps.
- Enemy cannot spawn with insufficient budget.
- Enemy spawn reason logged.
- Enemy does not expose hidden info in normal UI.

### Acceptance criteria

- Enemy behavior changes by difficulty profile.
- Enemy spawn no longer one-for-one direct response unless profile/budget/cooldown allow.
- Team cap works.
- Spawn reasons are readable.

### Rollback risks

High. Keep old enemy prototype behind a debug fallback until new behavior is stable.

---

## Gate 8 — SquadLeaderBrain shadow tasks

### Goal

Assign member tasks in debug/shadow mode without forcing all individual behavior.

### Files likely touched

```text
Assets/Scripts/Simulation/War/Command/SquadLeaderBrain.cs       (new)
Assets/Scripts/Simulation/War/Command/MemberTaskController.cs   (new stub)
Assets/Scripts/Simulation/War/Command/MemberRoleActionCatalog.cs(new)
Assets/Scripts/Simulation/War/WarTeamEntities.cs
```

### Data contracts added

```text
SquadLeaderTaskState
SquadBlackboard
MemberTaskType
MemberTaskStatus
MemberTask
ReactionTrigger
ReactionPolicy
```

### Code changes

- Build squad blackboard.
- Assign leader state based on mission.
- Assign shadow member tasks.
- Log task assignment/failure.
- Show member tasks in debug UI.
- Do not yet change physical member behavior unless already safe.

### Tests/smokes

- Scout patrol receives observe/mark/hold tasks.
- Engineer crew receives worker/guard split.
- Supply team receives carry/resupply tasks.
- Low ammo produces request/resupply task.
- Leader down triggers fallback state.

### Acceptance criteria

- Member tasks visible and role-appropriate.
- No gameplay break from task shadow mode.
- Task failure reasons appear in debug.

### Rollback risks

Medium. Disable shadow task generation.

---

## Gate 9 — Member task active subset

### Goal

Let a small, safe set of member tasks influence posture/movement/work.

### Files likely touched

```text
Assets/Scripts/Simulation/War/Command/MemberTaskController.cs
Assets/Scripts/Simulation/War/WarTeamSlice.cs
Assets/Scripts/Simulation/War/WarTeamEntities.cs
```

Active tasks:

```text
MoveToSquadTarget
HoldCover
ObserveArc
DigTrench
ImproveTrench
CarrySupply
ResupplySquad
TreatWounded
RegroupOnLeader
WithdrawToSafePoint
```

### Tests/smokes

- Member posture changes to match `HoldCover`.
- Engineer work task progresses correct build target.
- Porter/supply task closes ammo request.
- Medic task improves wounded state if existing sim supports it.
- Member task interruptions occur under contact.

### Acceptance criteria

- Active tasks produce small expected behavior changes.
- No member receives forbidden role task.
- Emergency reactions interrupt exposed work.

### Rollback risks

High. Keep active member tasks behind feature flag.

---

## Gate 10 — Future teams and hardpoints

### Goal

Add MG, mortar, aid, command/signals missions only after the system is stable.

### Files likely touched

```text
Assets/Scripts/Simulation/War/WarSquadAndHardpointCatalog.cs
Assets/Scripts/Simulation/War/Command/CommandMissionCatalog.cs
Assets/Scripts/Simulation/War/Command/MemberRoleActionCatalog.cs
Assets/Scripts/Simulation/War/Command/PlayerGeneral.cs
Assets/Scripts/Simulation/War/Command/EnemyGeneral.cs
```

### Code changes

- Add mission entries: `OccupyRifleBay`, `ClaimBuildMgPoint`, `MortarSupport`, `CasualtyResponse`, `CommandRelay`.
- Add role task support: MgGunner, TrenchMortarCrew, FieldDoctor, Signaller, ArtilleryObserver, TrenchLieutenant.
- Add hardpoint compatibility and claim slots.

### Tests/smokes

- MG crew occupies MG point and requests ammo.
- Mortar only acts on support request/marked contact.
- Aid team responds to medical request.
- Command team relays support requests.
- No hidden enemy info leaks.

### Acceptance criteria

- Each new team has a mission and debug reason.
- Each hardpoint has claim/socket rules.
- No all-50-template activation.

### Rollback risks

High. Add one future team family at a time.

---

## Recommended gate order

```text
1. Shadow contracts/log
2. Player mission assignment
3. Debug UI
4. Mission controller bias
5. Claims
6. Retasking
7. Enemy General
8. Squad leader shadow tasks
9. Member task active subset
10. Future teams/hardpoints
```

---

## Gate 1 Codex task wording

```text
Add a shadow command/tasking foundation for TWB Trenchworks. Create minimal command enums/classes for squad missions, mission status, mission priority, general intent, difficulty tier, assignment score breakdown, and command event log. Add a WarCommandDirector stub that can receive OnWarTeamSpawned and record command events, but do not alter existing WarTeamSlice decision behavior or enemy response behavior. Wire it only enough that player spawned squads can be observed in the event log. Keep all behavior deterministic and compile-safe.
```

---

## Pushback

Trying to implement Player General, Enemy General, squad leader tasks, member reactions, debug UI, and all future team templates in one pass is too broad. It will create hidden bugs and make Bob unable to tell whether a squad failed because of mission scoring, pathing, contact, claims, supply, or member tasks.

Gate 1 should be boring. That is the point.
<!-- END FILE: 11_implementation_gates.md -->

<!-- BEGIN FILE: 12_tests_smokes_and_acceptance_criteria.md -->
# 12 — Tests, Smokes, and Acceptance Criteria

## Purpose

This file defines deterministic smoke tests and manual Play Mode checks for the command/tasking system.

The test plan should prove:

- player squads get missions
- enemy spawns are budgeted and difficulty-driven
- squad leader states are sensible
- member tasks/reactions are role-appropriate
- claims prevent duplicate hardpoint/socket/support chaos
- retasking does not thrash
- no hidden enemy info leaks into normal UI/minimap

---

## General testing rules

Use fixed simulation seed, fixed difficulty profile, fixed lane selection, fixed spawn order, fixed tick count, and stable tie-breakers. Avoid wall-clock time, unseeded randomness, input timing dependency, and UI-only assertions when simulation state can be checked directly.

Suggested verification options, depending on current project patterns:

```text
Unity Test Runner:
  EditMode tests for catalogs/scoring/claims
  PlayMode tests for spawn/mission/squad loop

Dev menu:
  TWB/Debug/Run Command System Smoke
  TWB/Debug/Dump Command State
  TWB/Debug/Force Enemy Budget
  TWB/Debug/Force Support Request
```

If no automated test harness exists, add small deterministic debug menu checks before adding deeper behavior.

---

## Gate 1 tests — contracts and event log

### Test: event log ring buffer

Setup: create log with max entries 4. Add 6 events.

Expected:

- log contains latest 4
- event IDs stable/increasing
- no null summary errors

### Test: mission data default safe

Setup: create default `WarSquadMission`.

Expected:

- `Type = None`
- `Status = Pending` or safe default
- no target required
- serialization/debug formatter handles missing target

### Manual smoke

1. Start Play Mode.
2. Spawn each live player team from WAR tray.
3. Confirm no behavior change.
4. Confirm command event log can show spawn observation.

---

## Gate 2 tests — Player General assigns spawned squads

### Scout assignment

Setup: lane Center selected, no contact, no scout claim, spawn `scout_patrol`.

Expected: exactly one mission assigned; mission type is `ScoutProbe` or valid scout fallback; target lane is Center if valid; reason includes low visibility or selected lane; event `Command.MissionAssigned`.

### Assault assignment

Setup: lane Center selected, front pressure moderate, spawn `assault_section`.

Expected: mission `AssaultLine` or `HoldFightingLine`; reason references pressure/selected lane/front need; likely outputs include `Attack`, `Suppress`, `Hold`, or `Occupy`.

### Engineer assignment

Setup: lane North selected, weak trench depth or open blueprint, spawn `fortify_engineers`.

Expected: mission `DigIn`, `ImproveTrench`, or `BuildConnectTrench`; target is valid; reason references trench/build need.

### Supply assignment

Setup: ammo support request exists, spawn `supply_team`.

Expected: mission `SupplyResupply`; support request claim created if claims gate exists; reason references ammo/support request.

### Fallback assignment

Setup: no valid front target, spawn any team.

Expected: safe fallback mission, no crash, reason states fallback cause.

---

## Gate 3 tests — debug UI

For each live team:

1. Spawn squad.
2. Select squad.
3. Confirm mission, status, assignment reason, order, tactical phase, and recent command event are visible.
4. Destroy or remove squad if supported.
5. Confirm UI does not throw errors.

Normal UI must not show enemy hidden budget, hidden spawn candidate, hidden mission target, or hidden enemy team kind before contact. Debug mode may show it.

---

## Gate 4 tests — mission controller decision bias

### Scout mission bias

Setup: scout assigned `ScoutProbe`.

Expected decisions include `Scout`, `Occupy`, `Hold`, `MarkUnresolved`. Not expected as first choice unless emergency: `Attack`, `BuildHardpoint`, `Resupply`.

### Engineer mission bias

Setup: engineer assigned `BuildConnectTrench` with valid trench piece.

Expected decisions include `ConnectTrenches`, `DigIn`, `ImprovePosition`, `Hold`.

### Supply mission bias

Setup: supply team assigned `SupplyResupply` with valid support request.

Expected decisions include `Resupply`, `Hold`, and `Regroup` if unsafe.

### Emergency override

Setup: engineer building, confirmed contact appears, team pinned.

Expected: mission bias does not force continued build; decision can become `Hold`, `RequestSupport`, `Withdraw`, or `Regroup`; reason logged.

---

## Gate 5 tests — hardpoint reservation

### Duplicate engineer hardpoint claim

Setup: one MG build socket available, spawn two engineer teams.

Expected: first team claims socket; second team gets different target or fallback; claim denied event logged if attempted.

### Claim expiration

Setup: team claims trench socket but cannot path or makes no progress until TTL.

Expected: claim expires, `Command.ClaimExpired` logged, target becomes available.

### Release on completion

Setup: engineer completes build target.

Expected: claim released or transferred, mission completed, hardpoint available for occupy mission.

---

## Gate 6 tests — anti-stall and retask

| Test | Setup | Expected |
|---|---|---|
| No safe path retask | mission target unreachable, no safe path persists threshold | mission retasks/fails into `RegroupWithdraw` or alternate target; reason `NoSafePathThreshold`; old claim released |
| Contact escalation retask | scout on `ScoutProbe`, contact becomes `Confirmed` | scout retasks or phase changes to `MarkContact`; cooldown prevents loop |
| Support request retask | supply team on reserve, nearby ammo request appears | supply retasks to `SupplyResupply`; request claimed |
| No thrashing | candidates alternate close scores | no retask unless replacement beats current margin; cooldown works |

---

## Gate 7 tests — Enemy General spawn and difficulty

### Difficulty affects spawn rate

Run same seed for fixed ticks under `Recruit`, `Regular`, `Veteran`, and `Brutal`.

Expected: Recruit spawns fewer/slower than Regular; Veteran/Brutal spawn more/faster but respect caps; all spawns have reasons.

### Budget blocks spawn

Setup: enemy budget below cheapest valid cost, pressure high.

Expected: no spawn; event `Command.EnemySpawnBlocked reason=InsufficientBudget`.

### Cap blocks spawn

Setup: active enemy teams at hard cap.

Expected: no spawn; event `Command.EnemySpawnBlocked reason=HardTeamCap`.

### Response delay

Setup: player spawns at tick T, enemy pressure event recorded, response delay > 0.

Expected: no pressure-response spawn before T + delay; eligible after delay if budget/cap/cooldown allow.

### Fair information

Setup: hidden player support request not visible to enemy on Recruit/Regular.

Expected: enemy spawn reason does not cite hidden support request; normal UI does not leak internal enemy knowledge.

---

## Gate 8 tests — Squad leader creates member tasks

| Squad | Mission | Expected member tasks |
|---|---|---|
| Scout Patrol | `ScoutProbe` | Scout -> `ObserveArc`/`MarkContact`; PatrolCorporal -> movement/leadership; Rifleman -> `HoldCover`/guard; no primary build task. |
| Assault Section | `HoldFightingLine` | Riflemen -> `HoldCover`/`FireAtContact`; Medic -> `TreatWounded` only if casualty; leader -> support/regroup behavior. |
| Fortify Engineer | `BuildConnectTrench` | Sapper/FieldEngineer -> build/improve; Rifleman/Scout -> guard/observe; Porter -> supply. |
| Supply Team | `SupplyResupply` | QuartermasterRunner -> route/resupply lead; Porter -> `CarrySupply`; guard -> `HoldCover`. |

---

## Gate 9 tests — member reaction trees

| Test | Setup | Expected |
|---|---|---|
| Being attacked | member working on build task, contact/suppression begins | exposed work interrupts; member chooses `HoldCover` or role combat response; reason logged |
| Seeing/hearing enemy | scout hears suspected enemy | scout chooses `ObserveArc`; contact may become suspected; support roles do not overcommit |
| Low ammo | MG gunner or rifleman ammo low | high-use actions reduce/pause; ammo request raised; supply mission can claim |
| Wounded teammate | rifleman wounded near combat medic | medic gets `TreatWounded` if safe; guard may get `GuardMedic`; unsafe area pauses medical task |
| Leader down fallback | leader flag member down | fallback selected by deterministic priority; mission pauses/regroups; event logged; no fallback -> `RegroupWithdraw` |

---

## Gate 10 tests — future hardpoints/teams

| Feature | Setup | Expected |
|---|---|---|
| MG point | MG point built, MG crew spawned | mission occupy/hold; MgGunner `OperateMachineGun`; porter ammo task; low ammo request works |
| Mortar support | mortar pit, marked contact/support request, mortar team | `MortarSupport`; no action without request/mark; no hidden target use on low difficulty |
| Aid response | wounded squad raises medical request, aid team spawned | `CasualtyResponse`; doctor/medic/stretcher tasks; request closes on success |
| Command relay | command/signals hardpoint, weak support chain | `CommandRelay`; signaller/lieutenant tasks; support routing improves if implemented |

---

## No hidden enemy information leak

In normal play UI/minimap:

- hidden enemy mission targets not shown
- hidden enemy budget not shown
- hidden enemy spawn reason not shown
- hidden enemy team kind not shown before contact
- debug-only labels hidden unless debug enabled

Automated check if possible: search player-facing view model for enemy internal fields when debug flag is false. Expected: `EnemyGeneralBudget`, `EnemySpawnCandidate`, and `EnemyMissionReason` are hidden.

---

## Acceptance criteria summary

The command/tasking system is acceptable when:

1. Every spawned squad gets one bounded mission or fallback.
2. Missions have readable assignment reasons.
3. Enemy spawn behavior is budgeted, capped, delayed, and difficulty-tuned.
4. Squads can be retasked without thrashing.
5. Claims prevent duplicate small target chaos.
6. Member tasks are role-appropriate and deterministic.
7. Emergency reactions override exposed work.
8. Debug UI shows mission, leader state, member task, support request, claim, and failure reason.
9. Normal UI does not leak hidden enemy info.
10. Existing simulation authority remains in C# war simulation.

---

## Failure signs

Stop and fix before adding more depth if squads frequently have no mission, mission reasons are blank, enemy spawns feel instant/perfect on low difficulty, retasking happens every few ticks, multiple engineers claim same socket, supply teams all chase one request, member tasks contradict roles, Bob cannot tell why a squad stalled, or `WarTeamSlice.ChooseDecisionCore(...)` becomes a giant AI monolith.
<!-- END FILE: 12_tests_smokes_and_acceptance_criteria.md -->

<!-- BEGIN FILE: 13_open_questions_and_risk_register.md -->
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
<!-- END FILE: 13_open_questions_and_risk_register.md -->
