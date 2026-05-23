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
