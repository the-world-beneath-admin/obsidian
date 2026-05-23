# TWB Trenchworks Command Plan Gate 9 Progress Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks standalone Unity project

## Summary

Gate 9 first batch is implemented and verified. This pass focused on the lowest-risk active task effects: supply/ammo role tasking, the existing live supply delivery hook, and rifle-bay tasking/bonus proof. MG active fire was left unchanged because the man-emplacement mode already spends ammo, suppresses/damages only targets in arc, and has dedicated smoke coverage.

## What Changed

- Refined `SupplyResupply` member task assignment:
  - `AmmoRunner` and `ShellRunner` now map to `FetchAmmo`.
  - supply-capable leaders and `QuartermasterRunner` now map to `ResupplySquad`.
  - `Porter` now maps to `CarrySupply`.
  - unsupported roles still fall back to `HoldCover`.
- Added a scenario-only supply delivery helper so the existing `DeliverSupplyIfAdjacent` path can be smoke-tested without duplicating logistics logic.
- Expanded `MemberTaskActiveSubsetSmoke` to prove:
  - scout observe/mark posture behaviour still applies,
  - engineer trench-work posture behaviour still applies,
  - supply role task mapping is deterministic,
  - the existing supply delivery hook restores ammo to a nearby needy friendly squad,
  - `OccupyRifleBay` assigns leader observation and rifleman fire tasks,
  - a completed/manned rifle bay still improves rifle hit chance.
- Wired `MemberTaskActiveSubsetSmoke` into `TWB Trenchworks/Run Command Plan Smoke Test`.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\SquadLeaderBrain.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\MemberTaskActiveSubsetSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Tests And Checks Run

- Unity batchmode compile:
  - Passed.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-gate9-compile.log`
- Direct compiled-assembly command smoke set:
  - `WarCommandPlanDiagnosticsSmoke`: passed.
  - `WarCommandPlanRuntimeAliasSmoke`: passed.
  - `WarCommandPlanMissionProfileSmoke`: passed.
  - `WarMissionFamilyTaskCoverageSmoke`: passed.
  - `MemberTaskActiveSubsetSmoke`: passed.
  - `WarManEmplacementModeSmoke`: passed.
- Unity executeMethod command smoke:
  - Passed with `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunCommandPlanSmokeTest`.
  - Log: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-gate9-command-smoke.log`

## Cleanup Performed

- No scratch source files were created.
- Unity temp logs were left in the project `Temp` folder as verification evidence for this pass.

## Risks

- This is only the first Gate 9 batch. It does not complete casualty stabilization/carry, hardpoint repair, mortar/observer/signaller loops, or expanded MG-ammo behaviour.
- The live `supply_team` prototype does not yet include an `AmmoRunner`, so the smoke proves the `AmmoRunner -> FetchAmmo` resolver path directly and proves current runtime supply-team tasking through `QuartermasterRunner` and `Porter`.
- `DeliverSupplyForScenario` is intentionally scenario-only; production logistics still use the existing private `DeliverSupplyIfAdjacent` call inside `ApplyDecision`.

## Memory-Worthy Notes

- Gate 9 should proceed in small behaviour batches. Supply/ammo and rifle-bay tasking are now covered; MG should remain isolated to the man-emplacement smoke until a dedicated ammo-feed model exists.
- The live supply-team composition is `QuartermasterRunner`, two `Porter` members, and one `Rifleman`; planned supply units contain richer ammo-runner roles but are not all live runtime templates yet.

## Follow-Up Recommendations

1. Implement Gate 9 batch two: casualty stabilization and carry tasks.
2. Implement Gate 9 batch three: hardpoint build/repair effects beyond current trench/emplacement scaffolding.
3. Implement Gate 9 batch four: mortar, observer, and signaller loops.
4. Add live runtime support for at least one ammo-runner supply unit before trying to model sustained MG/mortar ammunition chains.
