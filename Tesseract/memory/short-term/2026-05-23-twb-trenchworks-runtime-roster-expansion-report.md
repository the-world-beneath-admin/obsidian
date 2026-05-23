# TWB Trenchworks Runtime Roster Expansion Report

Date: 2026-05-23

Scope: Standalone TWB Trenchworks Unity project, war-side runtime squad roster. This does not cover The World Beneath main game, Glassroot Garden, Alchemy, or shared platform work.

## What Changed

This pass fixed the first major blocker from the war-side readiness audit: only four squad profiles were runtime-runnable.

The runtime war team slice now loads the planned 50-template squad catalog in addition to the original four prototype templates. Planned template IDs now resolve to themselves through the command-plan compatibility layer, so planned squads can be spawned directly instead of being treated as locked catalog-only records.

The command-plan smokes were updated to match the new contract:

- prototype IDs still spawn
- planned aliases still spawn
- planned alternates now spawn instead of being blocked
- planned-only templates now spawn instead of being blocked
- a new coverage check spawns every planned template from `WarSquadAndHardpointCatalog.CreatePlannedSquadTemplates()`

## Files Touched

- `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Assets/Scripts/Simulation/War/WarTeamSlice.cs`
- `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Assets/Scripts/Simulation/War/Command/WarCommandPlanCompatibilityCatalog.cs`
- `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Assets/Scripts/Simulation/War/Command/WarCommandPlanRuntimeAliasSmoke.cs`
- `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Assets/Scripts/Simulation/War/Command/WarCommandPlanMissionProfileSmoke.cs`

## Checks Run

- `dotnet build TWB-TrenchWorks.sln --no-restore`
  - Passed with 0 warnings and 0 errors.

- Unity batch command-plan smoke:
  - Log: `C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks/Logs/codex-runtime-roster-command-smoke.log`
  - Passed with return code 0.
  - Key output:
    - `templateProfiles=50/True`
    - `runnableProfiles=50`
    - `plannedAlternateSpawns=True`
    - `plannedOnlySpawns=True`
    - `allPlannedSpawns=True`
    - `mission profile smoke passed=True`
    - `member task active subset smoke passed=True`
    - `man emplacement mode smoke passed=True`
    - `support emplacement brain smoke passed=True`

## Cleanup Performed

- Closed the child explorer agents after their read-only findings were integrated.
- No broad cleanup was performed.
- No permanent Obsidian wiki/index/hot/log files were edited.

## Remaining Risks

This pass makes all 50 planned squad templates runtime-spawnable. It does not mean all 50 have bespoke mature mission brains.

Known remaining issues:

- Mission-family implementation still includes partial and placeholder entries.
- Member tasks for broad planned families are still partly shadow/coverage logic rather than fully bespoke per-member execution.
- The enemy general now has more runnable squad IDs available, but richer difficulty-based selection and mission-family use still need a follow-up pass.
- Asset runtime acceptance is still incomplete. A child audit found many candidate packs are not referenced by runtime path factories and several loaders still rely on loose `Application.dataPath` paths.
- Full simulation smoke was not rerun in this pass because the previous audit's fresh rerun hung before smoke output. The next pass should either isolate that hang or run a narrower simulation smoke.
- No Unity Play Mode/F9 visual proof was performed in this pass.

## Memory-Worthy Notes

- War-side command-plan smoke now reports `runnableProfiles=50`; this supersedes the earlier `runnableProfiles=4` audit result for the runtime spawnability slice.
- The roster is runtime-spawnable, but play readiness still depends on mission hardening, enemy-general usage, asset runtime proof, support-emplacement depth, full simulation smoke, and visible Play Mode/F9 validation.

## Recommended Next Gate

Next implementation gate should be mission-family hardening for the newly runnable roster:

1. Add a runtime smoke that spawns representative squads from each major family and confirms each receives a non-`None` mission and visible squad/member task output.
2. Tighten `SquadMissionController` and `SquadLeaderBrain` for MG, mortar, aid, command, obstacle, and specialty squads.
3. Add enemy-general selection coverage so the enemy can choose from the broader runtime roster by difficulty and reaction context.
4. Then resume asset runtime registry/build-safe loader work.
