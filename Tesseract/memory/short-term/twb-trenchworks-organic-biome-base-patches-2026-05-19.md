# TWB Trenchworks Organic Biome Base Patches

Scope: TWB Trenchworks only.

## What Changed

- Replaced per-chunk random biome tile selection with deterministic low-frequency patch selection.
- Base terrain now groups 8x8 chunks into larger seeded patches, roughly 3-7 chunks wide, with jittered region boundaries.
- Added a read-only `WarWorld.Seed` so base terrain patch layout rerolls with the war map and remains stable during a run.
- Removed the war map draw calls for decorative terrain floor and tactical feature overlays, so rocks/outcrops/old feature blobs no longer render during base-tile review.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`

## Tests And Checks

- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.

## Cleanup

- Child subagent was closed after completion.
- No permanent Obsidian memory was updated.

## Risks

- Live Unity Play Mode visual QA is still required.
- Patch size may need tuning after viewing desert specifically, since desert makes hard rectangular transitions more obvious.

## Follow-Up Recommendation

Use `F5`, `F6`, and `F7` in Play Mode to inspect the new terrain patches. If desert still reads too grid-like, increase `WarGroundBasePatchChunkCells` from 4 to 5 or 6, or add soft transition overlay art later when the base layer is approved.
