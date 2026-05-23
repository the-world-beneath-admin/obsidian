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
