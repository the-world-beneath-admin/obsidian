# TWB Trenchworks Command System Gate 6 Progress Report

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity project
Worker: Bob / TWB Trenchworks standing worker

## Objective

Continue the command/tasking implementation plan with Gate 6: add conservative mission retask detection without creating a broad new behaviour system.

## What Changed

- Added mission retask state helpers to `WarSquadMission`.
- `WarCommandDirector` now evaluates retask signals after each tactical slice tick.
- First implemented retask rule:
  - player missioned squad becomes combat-ineffective or has fewer than two living members
  - command layer retasks the mission to `RegroupWithdraw`
  - mission status becomes `Retasking`
  - mission priority becomes `Emergency`
  - retask is locked briefly to avoid event spam
  - `MissionRetasked` command event is logged
- Added a cautious repeated no-progress rule:
  - if a missioned team has repeated stalls and no recent meaningful action, retask to `RegroupWithdraw`
- `WarTeamSnapshot.ActiveMissionReason` now exposes retask reason when present.
- Added `WarMissionRetaskSmoke` to verify event logging, mission state, and visible retask reason.
- Wired the retask smoke into the Unity editor smoke runner.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandTypes.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandDirector.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarMissionRetaskSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarMissionRetaskSmoke.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Tests And Checks Run

- Temporary pure C# simulation smoke harness:
  - `WarCommandEventLogSmoke.RunPrototypeSmoke()` passed.
  - `WarSquadMissionControllerSmoke.RunPrototypeSmoke()` passed.
  - `CommandClaimRegistrySmoke.RunPrototypeSmoke()` passed.
  - `WarMissionRetaskSmoke.RunPrototypeSmoke()` passed.
  - Output included:
    - `mission retask smoke passed=True, event=True, state=True, reason=True`
- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Result: passed, 0 warnings, 0 errors.
  - Note: solution build remains light/no-op; pure simulation harness remains the stronger check.
- Unity editor log scan for `error CS`, `Compilation failed`, and `Scripts have compiler errors`
  - Result: no matching compile errors found.

## Cleanup Performed

- Removed temporary compile/smoke harness folder:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\CommandCompileSmoke`

## Risks

- Retask behaviour is intentionally narrow. It handles clear safety failure, not full tactical replanning yet.
- The repeated no-progress retask rule is present but lightly covered compared with the combat-ineffective smoke.
- Mission status remains `Retasking` after retask; a later gate should decide when a squad returns to `Active` or receives a fresh mission.

## Memory-Worthy Notes

- The command layer now has its first real anti-stall safety hook: missioned squads can be redirected to `RegroupWithdraw` when they can no longer prosecute their mission.
- This is still subordinate to `WarTeamSlice`; command retask changes mission intent and hinting, not low-level movement/fire/build mechanics.
- Future retask expansion should use claim registry release signals, unresolved support requests, and sustained contact escalation.

## Follow-Up Recommendations

1. Implement Gate 7 enemy general as a shadow evaluator before replacing the legacy delayed response loop.
2. Add a mission status lifecycle pass so `Retasking` can resolve into `Active`, `Completed`, or `Failed`.
3. Add smokes for repeated no-progress retask and claim-release-driven retask.
