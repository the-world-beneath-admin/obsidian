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
