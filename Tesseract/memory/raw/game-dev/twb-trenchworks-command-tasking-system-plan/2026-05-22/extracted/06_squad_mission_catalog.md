# 06 — Squad Mission Catalog

## Purpose

The mission catalog bounds the command system. Every general assignment should map to a known mission. Every mission should map to a limited set of likely `TeamDecisionKind` outputs.

The goal is not free-form behavior. The goal is readable, deterministic mission execution.

---

## Catalog rules

Every mission needs:

- mission id
- allowed team kinds
- intended front depth
- required/desired hardpoint family
- prerequisites
- success condition
- failure condition
- retask triggers
- likely `TeamDecisionKind` outputs

Recommended ID format:

```text
mission.scout.probe
mission.scout.mark_contact
mission.assault.line
mission.line.hold_fighting
mission.hardpoint.occupy_rifle_bay
mission.engineer.dig_in
mission.engineer.improve_trench
mission.engineer.build_connect_trench
mission.hardpoint.claim_build_mg_point
mission.supply.resupply
mission.medical.casualty_response
mission.support.mortar
mission.command.relay
mission.regroup.withdraw
mission.reserve.hold
```

---

## Front depth vocabulary

| Depth | Meaning |
|---|---|
| Front | Active fighting/contact line. |
| Support | Behind or adjacent to front; supports squads/hardpoints. |
| Rear | Safer logistics or command area. |
| Any | Mission may choose best valid depth. |

---

## Hardpoint family vocabulary

Use existing families from the project prompt: rifle/firing bay, front-line empty MG point, mortar pit, aid/doctor point, supply cache/depot, observation/signals, obstacle/wire/mines, engineering workshop/dugout, command dugout, sanitation/sustainment, occult/ward support, and breach/pressure socket.

Phase 1 should focus on rifle/firing bay, front-line empty MG point, supply cache/depot, observation/signals, and engineering workshop/dugout. Mortar, aid, command, occult/ward, and breach/pressure should stay future until the base mission/task loop is stable.

---

## Bounded mission catalog table

| Mission ID | Mission type | Allowed team kinds | Intended depth | Hardpoint family | Prerequisites | Success condition | Failure condition | Retask triggers | Likely `TeamDecisionKind` outputs |
|---|---|---|---|---|---|---|---|---|---|
| `mission.scout.probe` | `ScoutProbe` | Scout, Command future limited | Front/Support | observation/signals desired | safe path or acceptable risk; lane needs visibility | lane contact becomes `Suspected`/`Confirmed`, or scout reaches probe target | no safe path, pinned too long, severe casualties | confirmed heavy contact, no path, probe complete, lane overstacked | Scout, Occupy, Hold, MarkUnresolved, Withdraw, Regroup |
| `mission.scout.mark_contact` | `MarkContact` | Scout, Command, Mortar spotter future | Front/Support | observation/signals desired | suspected/confirmed contact exists | contact marked/held long enough for other squads/support | contact lost, scout suppressed, no safe path | contact consolidated, support request created, scout low supply | Scout, Hold, RequestSupport, MarkUnresolved, Withdraw |
| `mission.scout.screen_flank` | `ScreenFlank` | Scout, Assault limited | Front/Support | none; observation helpful | adjacent lane has pressure or unresolved contact | flank lane contact heat reduced or marked | flank contact overwhelms squad; no path | adjacent pressure changes, scout needed elsewhere | Scout, Hold, MarkUnresolved, Withdraw, Regroup |
| `mission.assault.line` | `AssaultLine` | Assault, MachineGun limited support | Front | rifle/firing bay desired | confirmed/suspected pressure; enough cohesion/supply | target line contested/held/consolidated | casualties high, out of ammo, no safe path, pinned too long | contact escalates, support request needed, front objective reached | Attack, Suppress, Bound, Flank, Assault, RequestSupport, Withdraw, Regroup |
| `mission.line.hold_fighting` | `HoldFightingLine` | Assault, MachineGun, Command limited, Scout emergency | Front | rifle/firing bay desired; MG desired | front sector needs defender; position exists or can be occupied | hold duration satisfied; contact held/consolidated | line collapses, no ammo, severe casualties | relieved, low ammo, new attack mission | Occupy, Hold, Suppress, RequestSupport, TreatCasualty, Withdraw, Regroup |
| `mission.hardpoint.occupy_rifle_bay` | `OccupyRifleBay` | Assault, MachineGun, Scout limited, Command limited | Front | rifle/firing bay required/desirable | built or claimable rifle/firing bay exists | squad occupies bay and holds through contact window | socket invalid, overrun, no safe path | bay completed and held, support needed, MG point available | Occupy, Hold, Suppress, RequestSupport, Withdraw |
| `mission.engineer.dig_in` | `DigIn` | FortifyEngineer, Assault emergency | Front/Support | engineering workshop desired | target position lacks cover; safe enough to work | trench/cover reaches minimum progress | contact too heavy, no safe path, build claim lost | cover complete, attack pressure, better build task | DigIn, Hold, RequestSupport, Withdraw, Regroup, Stall |
| `mission.engineer.improve_trench` | `ImproveTrench` | FortifyEngineer | Front/Support | engineering workshop desired | existing trench below desired depth/quality | trench improvement threshold reached | socket invalid, no supplies, contact too heavy | improvement complete, support request, MG build need | ImprovePosition, DigIn, Hold, RequestSupport, Stall |
| `mission.engineer.build_connect_trench` | `BuildConnectTrench` | FortifyEngineer | Support/Front | trench blueprint piece required | unconnected friendly positions; blueprint visible/claimable | connection completed or usable | no safe path, build blocked, duplicate claim | connection complete, contact escalation, supply shortage | ConnectTrenches, DigIn, ImprovePosition, Hold, RequestSupport, Stall |
| `mission.hardpoint.claim_build_mg_point` | `ClaimBuildMgPoint` | FortifyEngineer build; MachineGun occupy later | Front/Support | front-line empty MG point required | empty/started MG point; claim available; cover/support acceptable | MG point built or ready for crew | claim conflict, no supplies, contact too heavy | MG point complete, pressure changes, no path | BuildHardpoint, ImprovePosition, DigIn, Hold, RequestSupport, Stall |
| `mission.supply.resupply` | `SupplyResupply` | Supply, Porter-heavy future | Support/Front/Rear | supply cache/depot desired | ammo/supply request or low supply target; safe route | target resupplied above threshold | no safe path, target destroyed/withdrawn, supply depleted | request satisfied, higher request, team threatened | Resupply, Hold, RequestSupport, Withdraw, Regroup, Stall |
| `mission.medical.casualty_response` | `CasualtyResponse` | Aid; Assault emergency medic; Command limited | Support/Front | aid/doctor desired | wounded/casualty request; medical supplies | casualty treated/evacuated/stabilized | no safe path, medic down, target lost | request satisfied, team threatened, aid point full | TreatCasualty, Resupply, Hold, Withdraw, Regroup |
| `mission.support.mortar` | `MortarSupport` | Mortar, Command/Observer support | Rear/Support | mortar pit required/desirable | mortar team; support request/marked contact; ammo | support request serviced or contact disrupted in game terms | no ammo, no spotter/request, position threatened | request complete, ammo low, lane overrun | RequestSupport, Hold, Resupply, Withdraw, Regroup |
| `mission.command.relay` | `CommandRelay` | Command, Scout/Signaller limited | Support/Rear | command dugout or observation/signals desired | support chain weak, relay socket available | relay coverage active; support latency reduced | relay point invalid, command team threatened | front shifts, relay no longer needed, contact escalates | Hold, Occupy, RequestSupport, MarkUnresolved, Regroup |
| `mission.regroup.withdraw` | `RegroupWithdraw` | All | Any -> safer support/rear | regroup point desired | low cohesion, leader down, no safe path, pinned, low supply | squad reaches safe point and recovers threshold | no path, team destroyed, contact follows | recovered, new support route, emergency mission | Withdraw, Regroup, Hold, RequestSupport |
| `mission.reserve.hold` | `ReserveHold` | All | Support/Rear | depends on team kind | no higher-priority mission valid | team holds ready position; can accept retask | position threatened, support request appears, lane changes | new mission score higher, contact appears | Hold, Occupy, Resupply, TreatCasualty, Regroup |

---

## Required mission details

### `ScoutProbe`

Purpose: reveal or clarify lane state without committing heavy squads.

Allowed team kinds: Scout primary; Command future limited if signaller/observer composition exists.

Prerequisites: lane has low visibility or `ContactState.None/Suspected`, no existing scout probe claim in the same small sector, and a path exists or risk is acceptable.

Success: scout reaches probe target, contact state becomes `Suspected` or `Confirmed`, or lane is sufficiently observed for a time window.

Failure: no safe path, squad pinned beyond threshold, leader down with no fallback, casualties too high.

Likely outputs: `Scout`, `Occupy`, `Hold`, `MarkUnresolved`, `Withdraw`, `Regroup`.

### `MarkContact`

Purpose: turn suspected/confirmed contact into an actionable front/contact state. Allowed for Scout, Command with signaller/observer roles, and future spotting support. Success means contact remains marked/held through threshold and can be linked to support or assault/hold missions. Failure means contact lost, scout cannot observe, no safe observing position, or squad forced to withdraw.

### `AssaultLine`

Purpose: commit an assault/rifle team to pressure or contest a front line. Allowed for Assault primary; MachineGun only as support hold. Success means target line reaches held/consolidated state or squad occupies target fighting position. Failure means out of ammo, casualties too high, no safe path, pinned beyond recovery, or support request timeout.

### `HoldFightingLine`

Purpose: stabilize a lane/sector and prevent collapse. Allowed for Assault, MachineGun, Command limited, Scout emergency. Success means hold duration satisfied or contact held/consolidated. Failure means position overrun, ammo exhausted, no safe resupply, or severe casualties.

### `OccupyRifleBay`

Purpose: put a suitable squad in a rifle/firing bay. Allowed for Assault primary, MachineGun temporary, Scout observation, Command relay if safe. Success means squad occupies socket and bay remains held. Failure means socket invalid, claim conflict, heavy contact, or no safe path.

### `DigIn`, `ImproveTrench`, `BuildConnectTrench`

Purpose: create cover, improve trench quality, and connect positions. FortifyEngineer is primary. Success means trench/cover reaches threshold. Failure means invalid blueprint, duplicate claim, no supplies, no safe path, or contact too heavy.

### `ClaimBuildMgPoint`

Purpose: claim and build an MG point, or later assign MG crew to occupy one. Engineers build; MG crews occupy. Success means hardpoint built or crewed. Failure means claim denied, supply insufficient, support absent, or no safe path.

### `SupplyResupply`

Purpose: answer ammo/supply support requests and keep front squads useful. Success means target supply above threshold and support request closed. Failure means no safe route, target invalid, supply team depleted, or request already completed by another responder.

### `CasualtyResponse`

Purpose: answer medical pressure in a bounded, game-readable way. Aid teams are primary. Success means wounded stabilized, treated, or moved to aid point. Failure means no safe path, medic/doctor unavailable, target lost, or medical supplies depleted.

### `MortarSupport`

Purpose: let future mortar teams service fire-support requests through marked contacts and support chains. Success means support request serviced and ammo/cooldown updated. Failure means no ammo, no marked contact/spotter, mortar pit invalid, or team threatened.

### `CommandRelay`

Purpose: improve support routing, visibility, and command cohesion in a lane. Success means relay coverage active and selected lane has command coverage. Failure means relay socket invalid, team threatened, or no command/signals hardpoint.

### `RegroupWithdraw`

Purpose: every squad has a safe bounded fallback. Success means squad reaches regroup point and recovers threshold. Failure means no safe path, contact follows, or squad cannot move.

---

## Mission catalog implementation shape

Use static catalog entries at first:

```csharp
public sealed class MissionCatalogEntry
{
    public WarSquadMissionType Type;
    public string MissionId;
    public WarTeamKind[] AllowedTeamKinds;
    public FrontDepth IntendedDepth;
    public HardpointFamily RequiredOrDesiredHardpoint;
    public TeamDecisionKind[] LikelyDecisionOutputs;
    public string Notes;
}
```

Keep success/failure checks as named policy methods:

```text
MissionSuccessRules.IsScoutProbeComplete(...)
MissionFailureRules.IsMissionBlocked(...)
MissionRetaskRules.ShouldRetask(...)
```

Do not put all mission logic in one catalog object.

---

## Phase 1 mission scope

Implement active mission assignment for:

- `ScoutProbe`
- `MarkContact`
- `AssaultLine`
- `HoldFightingLine`
- `DigIn`
- `ImproveTrench`
- `BuildConnectTrench`
- `SupplyResupply`
- `RegroupWithdraw`
- `ReserveHold`

Keep these as future labels only until their teams exist:

- `ClaimBuildMgPoint`
- `MortarSupport`
- `CasualtyResponse`
- `CommandRelay`
- `OccupyRifleBay` if rifle bay sockets are not ready

---

## Pushback

The full catalog is useful, but Phase 1 should not attempt all missions at once. Start with the four live templates and the minimum fallback missions. Add MG/mortar/aid/command missions only after debug telemetry can clearly show why squads are assigned and retasked.
