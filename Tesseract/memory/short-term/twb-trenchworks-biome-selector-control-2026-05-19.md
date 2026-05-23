# TWB Trenchworks Biome Selector Control

Scope: TWB Trenchworks only.

## What Changed

- Added war tray biome controls for visual terrain review.
- Added optional biome override plumbing through `TrenchworksSimulation` and `WarWorld`.
- Normal startup can still choose a random biome.
- Manual biome selection pins the chosen biome and regenerates the war map.
- `ROLL` regenerates the same current biome with a fresh random seed.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`

## Tests And Checks

- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.

## Cleanup

- Child subagent was closed after completion.
- No permanent Obsidian memory was updated.

## Risks

- Unity Play Mode click-through/visual verification has not yet been run.
- Bottom tray crowding should be checked at the live target resolution.

## Follow-Up Recommendation

Use Play Mode to test `TEMP`, `JUNG`, `DES`, `BIO`, and `ROLL` while watching for map regeneration, biome persistence, and lower-tray readability.
