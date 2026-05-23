# TWB Trenchworks Command Plan Gate 5 Progress Report

Date: 2026-05-22
Scope: Standalone TWB-tagged Unity 2D game - TWB Trenchworks.

## What Changed

- Implemented scoped Gate 5 enemy mission assignment.
- Added `EnemyGeneral` command-layer mission assignment so enemy spawns no longer default to `NoActiveMission` when they enter through the integrated war facade.
- Enemy assignments use the same planned/prototype profile vocabulary and `CommandMissionCatalog` legal mission checks as the player-side command system.
- `WarCommandDirector.OnWarTeamSpawned(...)` now assigns enemy missions for enemy squads with a known team kind and logs `EnemyGeneralInitialAssignment`.
- Preserved current enemy tactical behaviour by gating `TryGetDecisionHint(...)` to player missions only. Enemy missions are now visible telemetry/command state, but they do not yet bias enemy squad tactical decisions.
- Extended command-plan mission-profile smoke to assert enemy assignments are profile-backed and non-`None`.
- Extended enemy-general shadow smoke so future broad smoke runs also require spawned enemy responses to expose real missions.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\EnemyGeneral.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\EnemyGeneral.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandDirector.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\WarCommandPlanMissionProfileSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\EnemyGeneralShadowEvaluatorSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\PlayerGeneral.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`

## Checks Run

- `dotnet build .\TWB-TrenchWorks.sln --no-restore`
  - Passed with 0 warnings and 0 errors.
- Unity batch command-plan smoke:
  - `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunCommandPlanSmokeTest`
  - Passed.
  - Result summary:
    - compatibility passed `True`
    - aliases `4/True`
    - mission families `32/True`
    - template profiles `50/True`
    - Gate 3 profiles `True`
    - runtime alias smoke passed `True`
    - mission profile smoke passed `True`
    - scoring context `True`
    - enemy assignments `True`
- Unity batch broad simulation smoke:
  - `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest`
  - Failed on the pre-existing integrated front-establishment smoke before Gate 5-specific enemy mission proof could be reached.
  - Failure summary included `stage1Skeleton=False`, `dominoTopology=False`, `roles=False`, `assignmentHardpoint=False`, and `roleHardpointDepth=False`.

## Cleanup Performed

- No source files, user files, raw evidence, or reports were deleted.
- Unity generated the `.meta` file for the new `EnemyGeneral.cs`.
- Relevant smoke logs remain under:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-command-plan-gate5-smoke.log`
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\codex-command-plan-gate5-full-simulation-smoke.log`

## Risks

- Gate 5 is complete in scoped form for command telemetry/mission assignment, not full enemy tactical tuning.
- Enemy mission hints are intentionally gated off for this pass. A later gate can deliberately enable or tune enemy mission hints after tests exist.
- Broad simulation smoke still has an older front-establishment failure. That should remain tracked separately from command-plan Gate 5.

## Memory-Worthy Notes

- The safe Gate 5 seam is `WarCommandDirector.OnWarTeamSpawned(...)`, not the enemy budget/cooldown method.
- Enemy response spawning, budget, and difficulty remain in `TrenchworksSimulation`; mission assignment now lives in the command layer.
- Enemy squads now have active mission snapshots and logs, while their tactical behaviour remains unchanged until a later tuning gate.

## Follow-Up Recommendations

1. Gate 6 should verify every mission family has a minimum viable squad-leader/member-task plan or an explicit placeholder lock.
2. Do not enable enemy decision hints until enemy behaviour has its own targeted smoke.
3. Keep the old integrated front-establishment smoke failure separate; do not let it block command-plan gate progress unless the next gate depends on that front proof.
