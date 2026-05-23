# TWB Trenchworks Command Plan Gate 6 Progress Report

Date: 2026-05-22
Scope: Standalone TWB-tagged Unity 2D game - TWB Trenchworks.

## What Changed

- Implemented scoped Gate 6 squad-leader/member-task coverage.
- Added `MissionFamilyMemberTaskPlanCatalog` so every command-plan mission family maps to:
  - a leader task state,
  - primary member tasks,
  - fallback member tasks,
  - runnable/partial/placeholder status,
  - a visible reason.
- Extended `SquadLeaderBrain` with direct task-state coverage for:
  - `ClaimBuildMgPoint`,
  - `CasualtyResponse`,
  - `MortarSupport`,
  - `CommandRelay`.
- Added an explicit placeholder mission-family lock for `ScreenFlank`, since the enum exists but the runtime flank-screen behaviour is not implemented.
- Added `WarMissionFamilyTaskCoverageSmoke` to prove:
  - all mission families have task plans,
  - all planned profiles have primary/fallback task coverage,
  - placeholders expose visible locks,
  - leader-down fallback deterministically assigns regroup tasks,
  - every mission enum except `None` has either a command entry or a placeholder mapping.
- Wired the new Gate 6 smoke into `TWB Trenchworks > Run Command Plan Smoke Test`.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MissionFamilyMemberTaskPlanCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MissionFamilyMemberTaskPlanCatalog.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarMissionFamilyTaskCoverageSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarMissionFamilyTaskCoverageSmoke.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\SquadLeaderBrain.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanCompatibilityCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Checks Run

- `dotnet build .\TWB-TrenchWorks.sln --no-restore`
  - Passed with 0 warnings and 0 errors.
- Unity batch command-plan smoke:
  - `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunCommandPlanSmokeTest`
  - Passed.
  - Result summary:
    - compatibility passed `True`
    - aliases `4/True`
    - mission families `33/True`
    - template profiles `50/True`
    - placeholders `14`
    - Gate 3 profiles `True`
    - runtime alias smoke passed `True`
    - mission profile smoke passed `True`
    - scoring context `True`
    - enemy assignments `True`
    - mission family task coverage passed `True`
    - leader fallback `True`
    - unsupported states `True`

## Cleanup Performed

- No source files, user files, raw evidence, or reports were deleted.
- Unity generated `.meta` files for the two new command smoke/catalog scripts.
- Unity smoke log remains at:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-command-plan-gate6-smoke.log`

## Risks

- Gate 6 is coverage and deterministic task assignment, not full active member behaviour. Most tasks still apply safe posture effects only.
- `ScreenFlank` remains explicitly placeholder-locked.
- MG, mortar, aid, and command task plans now exist, but their active world-state effects remain later gates.
- Broad simulation smoke still has the previously reported front-establishment failure unrelated to this command-plan gate.

## Memory-Worthy Notes

- The command-plan task spine is now mission-family based instead of scattered only inside `SquadLeaderBrain`.
- Every planned profile primary/fallback family now has either a viable task path or a visible placeholder lock.
- Missing leader/key-role fallback remains deterministic through `RegroupOnLeader` / `HoldCover`.

## Follow-Up Recommendations

1. Gate 7 should implement the first emplacement proof for rifle bay and MG point only.
2. Gate 7 should make `OperateMachineGun`, `BuildHardpoint`, and rifle-bay hold/fire tasks affect actual emplacement state before expanding to mortar/aid/command.
3. Keep `ScreenFlank` locked until flank-screen tactical behaviour is deliberately designed and tested.
