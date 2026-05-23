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
