# TWB Trenchworks Command Plan Gate 9 Medical Batch Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity project

## Summary

Gate 9 medical active-task effects are implemented and directly smoke-tested. `TreatWounded` now changes world state by healing a wounded living squad member and consuming medical supply. `CarryStretcher` now changes world state by moving a wounded squad member back to the squad anchor.

## What Changed

- Added `WarSubUnit.IsWounded`.
- Added `WarSubUnit.RecoverHealth(int amount)`.
- Added `WarTeam.TryTreatWoundedMember(int tick)`.
- Added `WarTeam.TryCarryWoundedMemberToAnchor(int tick)`.
- Added `MemberTaskController.ApplyTeamTaskEffect(...)` for team-context active task effects.
- Updated `SquadLeaderBrain` so assigned member tasks can apply team-level effects after posture effects.
- Extended `MemberTaskActiveSubsetSmoke` with `medicalTasks=True` coverage.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamEntities.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskController.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\SquadLeaderBrain.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskActiveSubsetSmoke.cs`

## Tests And Checks Run

- Unity batchmode compile:
  - Passed.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-gate9-medical-compile.log`
- Direct compiled-assembly command smoke set:
  - `WarCommandPlanDiagnosticsSmoke`: passed.
  - `WarCommandPlanRuntimeAliasSmoke`: passed.
  - `WarCommandPlanMissionProfileSmoke`: passed.
  - `WarMissionFamilyTaskCoverageSmoke`: passed.
  - `MemberTaskActiveSubsetSmoke`: passed with `medicalTasks=True`.
  - `WarManEmplacementModeSmoke`: passed.

## Verification Note

The Unity executeMethod rerun for the medical batch did not emit the final smoke line in its log, likely because the project is already open in the interactive editor. The direct compiled-assembly smoke set did pass after the Unity compile, so the medical behaviour is verified at assembly level.

## Risks

- This is a modest prototype treatment model, not a complete casualty system. It heals wounded living members; it does not model evacuation queues, permanent dead, field hospitals, or long-term wounded states.
- `CarryStretcher` currently moves the most injured living member to the squad anchor. Aid-post routing belongs in Gate 10 support emplacement brains.

## Follow-Up Recommendations

1. Keep AidPost treatment queues and casualty evacuation as Gate 10 work.
2. Add richer wounded/casualty states before tuning death, revive, evacuation, or morale penalties.
3. Continue Gate 9 with hardpoint build/repair effects or mortar/observer/signaller effects next.
