# TWB Trenchworks F8 Manual Squad Pair

Scope: TWB Trenchworks only.

## What Changed

- Disabled automatic front wave spawning on play by default.
- Added `F8` as a manual test harness input.
- Each `F8` press spawns one random player integrated squad and one random enemy integrated squad.
- The pair uses a random `TOP`, `MID`, or `BOT` front lane.
- Existing `F5`, `F6`, and `F7` biome full-map regeneration remains intact and still creates fresh random review maps.
- Existing `F9` trench debug overlay remains intact.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`

## Tests And Checks

- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.

## Cleanup

- Child subagent was closed after completion.
- No permanent Obsidian memory was updated.

## Risks

- Unity Play Mode verification has not yet been run.
- Need to confirm `F8` is received by the Unity Game view and each press creates exactly one opposing pair without timed follow-up waves.

## Follow-Up Recommendation

In Play Mode, press `F5`, `F6`, or `F7` to generate a biome map, then press `F8` repeatedly while using `F9` debug overlay to evaluate trench access, hardpoints, routes, and squad movement without automated-wave noise.
