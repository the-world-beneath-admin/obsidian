# TWB Trenchworks Biome Patch Tuning

Scope: TWB Trenchworks only.

## What Changed

- Tuned biome base terrain patches to be slightly more varied after live visual feedback.
- Reduced patch region size from 4 chunks to 3 chunks.
- Added a named patch jitter constant and increased jitter from 0.72 to 0.86.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`

## Tests And Checks

- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.

## Cleanup

- Child subagent was closed after completion.
- No permanent Obsidian memory was updated.

## Risks

- Live Unity Play Mode visual QA is still required to confirm this lands between the previous checkerboard and the too-broad patch layout.

## Follow-Up Recommendation

Inspect desert first with `F7`, then temperate/jungle with `F5` and `F6`. If the desert still feels too uniform, try region size 2; if it drifts back toward checkerboard, return to 3 and adjust only jitter.
