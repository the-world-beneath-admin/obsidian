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
