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
