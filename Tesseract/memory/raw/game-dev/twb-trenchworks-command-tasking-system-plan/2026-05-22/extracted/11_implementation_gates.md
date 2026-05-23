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
