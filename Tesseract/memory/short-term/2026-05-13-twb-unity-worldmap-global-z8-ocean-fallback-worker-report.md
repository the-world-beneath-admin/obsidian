# TWB Unity Worker Report - 2026-05-13 - Worldmap Global Z8 Ocean Fallback

## Task

Implement the next bounded world-map generation slice for The World Beneath main Unity game: begin global z8/full-close-zoom tile generation, but repeat open-ocean tiles instead of creating every ocean PNG.

## Result

Added a reusable z8 ocean fallback path. The renderer now loads direct coordinate tiles first, then uses a generated ocean-only catalog to substitute one shared `ocean.png` for open ocean before falling back to hosted/cache/parent tiles.

Generated the global z8 ocean catalog and processed chunks 0 and 1 of 32:

- Chunk 0 (`y=0..7`) was pure ocean: 0 coordinate PNGs generated, 2,048 ocean-only tile requests skipped.
- Chunk 1 (`y=8..15`) generated 433 land/coast/feature coordinate PNGs on first run and skipped 1,615 ocean-only tile requests.
- A rerun of chunk 1 correctly skipped the existing 433 generated tiles rather than duplicating them.
- z8 Resources pack now has 543 coordinate PNGs plus 1 reusable ocean PNG.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\WorldMap\WorldMapOceanTileGeneratedCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\WorldMap\twb_ops_table_v1\z8\ocean.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\WorldMap\twb_ops_table_v1\z8\*.png` / `.meta` for the generated chunk-1 z8 coordinate tiles
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\ops-table\generate-global-z8-land-pack.py`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\generated\hosted\worldmap\v1\styled\8\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\diagnostics\worldmap\global_z8_land_ocean_report.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\diagnostics\worldmap\global_z8_land_ocean_chunk_000_of_032.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\diagnostics\worldmap\global_z8_land_ocean_chunk_001_of_032.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.Domain.csproj`

## Checks run

- `python tools\worldmap\ops-table\generate-global-z8-land-pack.py --chunk-count 32 --chunk-index 0`
- `python tools\worldmap\ops-table\generate-global-z8-land-pack.py --chunk-count 32 --chunk-index 1 --no-catalog`
- Reran chunk 1 with `--no-catalog`; it skipped 433 existing generated tiles and reported the existing 731 ocean ranges.
- Resource counts:
  - z5: 1,024 coordinate PNGs
  - z6: 4,096 coordinate PNGs
  - z8: 543 coordinate PNGs plus `ocean.png`
  - hosted z8 mirror: 543 coordinate PNGs
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 3 existing warnings and 0 errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` returned `Status: probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` was blocked because another Unity instance has the project open; automation summary still reported `Status: probably-clean`.

## Cleanup performed

No scratch files were created outside the intended generator output, diagnostics, Resources tile pack, hosted staging mirror, and this report. No unrelated user or worker edits were reverted.

## Risks

- Only 2 of 32 global z8 chunks have been processed; 30 chunks remain.
- Chunk-1 diagnostics now show the rerun state (`generatedTiles: 0`, `skippedExistingTiles: 433`) because the rerun intentionally refreshed the report after the generator bookkeeping fix.
- Unity batch compile still needs to be rerun after the open editor is closed or the editor-side compile finishes naturally.
- The repo worktree is already very dirty with many unrelated existing changes and untracked files; this pass did not attempt cleanup or staging.

## Memory-worthy notes

- Full z8 generation should not create every ocean tile. The accepted strategy is a generated ocean-only range catalog plus one reusable `Assets/Resources/WorldMap/twb_ops_table_v1/z8/ocean.png`.
- The next z8 generation work can resume with `--chunk-count 32 --chunk-index 2 --no-catalog` and continue through chunk 31.
- Use `--overwrite` only intentionally; the default path preserves existing Midwest detail and previously generated chunks.

## Do not promote to memory

Do not promote individual generated tile filenames, transient diagnostic timestamps, or the dirty-worktree noise.

## Next recommended gate

Run the next z8 chunks in controlled bands, starting with chunk 2 of 32, keeping the ocean fallback enabled and checking counts after each batch. Then run Unity compile once the editor is not blocking batchmode.
