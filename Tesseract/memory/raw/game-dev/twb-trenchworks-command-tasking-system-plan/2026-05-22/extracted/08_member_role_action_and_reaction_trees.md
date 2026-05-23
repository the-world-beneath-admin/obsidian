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
