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
