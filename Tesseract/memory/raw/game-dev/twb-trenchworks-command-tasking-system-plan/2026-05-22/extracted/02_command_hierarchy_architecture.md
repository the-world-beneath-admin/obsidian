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
