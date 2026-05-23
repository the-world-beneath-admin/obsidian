# TWB Trenchworks Command Plan Gate 9 Support Loop Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity project

## Summary

Gate 9 support-loop active task effects are implemented and directly smoke-tested. This pass gives observer, signaller, and mortar tasks visible team-level effects without trying to build the full future mortar emplacement brain.

## What Changed

- Added `WarTeam.TrySpotForSupportTask(int tick)`.
- Added `WarTeam.TryRelayCommandTask(int tick)`.
- Added `WarTeam.TryOperateIndirectFireTask(int tick)`.
- Updated `MemberTaskController.ApplyTeamTaskEffect(...)`:
  - `SpotForSupport` records support spotting state.
  - `RelayCommand` improves/refreshes team coordination state.
  - `OperateMortar` consumes ammo, records firing, and records fire-support activity.
- Extended `MemberTaskActiveSubsetSmoke` with `supportLoopTasks=True` coverage using a small scenario-only mortar/signaller team.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamEntities.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskController.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskActiveSubsetSmoke.cs`

## Tests And Checks Run

- Unity batchmode compile:
  - Passed.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-gate9-support-loop-compile.log`
- Direct compiled-assembly command smoke set:
  - `WarCommandPlanDiagnosticsSmoke`: passed.
  - `WarCommandPlanRuntimeAliasSmoke`: passed.
  - `WarCommandPlanMissionProfileSmoke`: passed.
  - `WarMissionFamilyTaskCoverageSmoke`: passed.
  - `MemberTaskActiveSubsetSmoke`: passed with `supportLoopTasks=True`.
  - `WarManEmplacementModeSmoke`: passed.

## Risks

- This is not the full mortar pit brain. It does not select targets, require a finished mortar hardpoint, resolve friendly-fire risk, or coordinate with a live observer line.
- `OperateMortar` currently records fire-support activity on the team itself. The future Gate 10 mortar brain should own actual target selection and fire mission resolution.

## Memory-Worthy Notes

- Gate 9 active task effects now cover supply/ammo, rifle-bay tasking, MG operation smoke, medical treatment/carry, and observer/signaller/mortar task state.
- The remaining hardpoint work is mostly already present as trench/blueprint/hardpoint progress in `WarTeamSlice`; a repair-specific model is still future.

## Follow-Up Recommendations

1. Treat hardpoint repair as a Gate 10/Gate 11 refinement unless a damaged-hardpoint state is introduced.
2. Start Gate 10 with support emplacement brain snapshots for mortar pit, aid post, command dugout, and supply cache/depot.
3. Keep mortar target selection behind a dedicated Gate 10 smoke rather than expanding the member-task controller further.
