# TWB Trenchworks Command System Gate 7 Progress Report

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity project
Worker: Bob / TWB Trenchworks standing worker

## Objective

Continue the command/tasking implementation plan with Gate 7: move the enemy general away from a simple one-for-one delayed response and toward budgeted, capped, difficulty-driven spawning.

## What Changed

- Added `EnemyDifficultyProfile`, `EnemyVirtualBudget`, `EnemySpawnCandidate`, and `EnemyInfoAccessLevel`.
- Added `EnemyDifficultyCatalog` with Recruit, Regular, Veteran, and Brutal profiles.
- Added `EnemyGeneralShadowEvaluator` and shadow decision summaries.
- `TrenchworksSimulation` now tracks:
  - enemy difficulty profile
  - virtual budget
  - pressure debt
  - spawn cooldown
  - profile hard cap
  - shadow-vs-legacy comparison counts
- Player spawns now add pressure debt and queue response delay from the active difficulty profile.
- Enemy responses now require:
  - pending response
  - response delay satisfied
  - spawn cooldown satisfied
  - hard team cap not reached
  - enough virtual budget for selected template
- Successful enemy spawns spend virtual budget and set the next allowed spawn time.
- Enemy spawn/block logs now include readable budget/cap/cooldown reasons.
- Added smokes for:
  - enemy general shadow comparison
  - difficulty profile ordering
  - budget overspend blocking
  - budget cooldown.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\EnemyGeneralShadowEvaluator.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\EnemyGeneralShadowEvaluator.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\EnemyGeneralShadowEvaluatorSmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\EnemyGeneralShadowEvaluatorSmoke.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\EnemyDifficultyCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\EnemyDifficultyCatalog.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\EnemyGeneralBudgetDifficultySmoke.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\Command\EnemyGeneralBudgetDifficultySmoke.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

## Tests And Checks Run

- Temporary pure C# simulation smoke harness:
  - `WarCommandEventLogSmoke.RunPrototypeSmoke()` passed.
  - `WarSquadMissionControllerSmoke.RunPrototypeSmoke()` passed.
  - `CommandClaimRegistrySmoke.RunPrototypeSmoke()` passed.
  - `WarMissionRetaskSmoke.RunPrototypeSmoke()` passed.
  - `EnemyGeneralShadowEvaluatorSmoke.RunPrototypeSmoke()` passed.
  - `EnemyGeneralBudgetDifficultySmoke.RunPrototypeSmoke()` passed.
  - Output included:
    - `enemy general shadow smoke passed=True`
    - `enemy budget difficulty smoke passed=True`
- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Result: passed, 0 warnings, 0 errors.
- Unity editor log scan for `error CS`, `Compilation failed`, and `Scripts have compiler errors`
  - Result: no matching compile errors found.

## Cleanup Performed

- Removed temporary compile/smoke harness folder:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\CommandCompileSmoke`

## Risks

- The old selector still chooses the final supported template; the new evaluator compares and the budget gate controls whether the spawn may happen.
- Lane scoring is still simple: pressure lane counts and recent player spawn inputs. Full fair-information pressure maps are not yet implemented.
- Enemy mission assignment currently relies on existing spawn observation and placeholder mission handling for enemy teams; richer enemy mission assignment remains future work.

## Memory-Worthy Notes

- Enemy general now has an actual budget/cooldown/profile gate and is no longer purely one-for-one once response delay is satisfied.
- Default difficulty is Regular.
- Supported enemy spawn templates remain the four live templates: scout, assault, fortify engineers, and supply.
- This is the proper bridge toward replacing the old loop, but the replacement should still be playtested before removing all legacy selection logic.

## Follow-Up Recommendations

1. Implement Gate 8 `SquadLeaderBrain` as shadow member-task assignment rows.
2. Add first-class enemy-general debug UI for difficulty, budget, next spawn, last block reason, and last spawn reason.
3. Expand enemy mission assignment so enemy squads receive typed missions instead of `NoActiveMission`.
