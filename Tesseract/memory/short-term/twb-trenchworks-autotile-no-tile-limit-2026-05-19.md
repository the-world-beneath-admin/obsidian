# TWB Trenchworks - Autotile No Tile Limit Update

Date: 2026-05-19
Scope: TWB Trenchworks only

## What Changed

- Removed the implied fixed `18-20` / `20` tile ceiling from the trench autotile tileset docs and prompts.
- Reframed the 16 cardinal neighbor-mask tiles as the minimum core set, not the full tileset.
- Added guidance that full production may require multiple named sheets or batches.
- Added expansion categories for:
  - edge/cap variants
  - spoil/detritus overlays
  - transition tiles
  - hardpoint/socket interfaces
  - trench width/style variants
  - damaged or under-construction variants

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-trench-autotile-tileset-spec-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\desert\tier1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\desert\tier2.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\desert\tier3.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\temperate_forest\tier1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\temperate_forest\tier2.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\temperate_forest\tier3.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\tropical_jungle\tier1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\tropical_jungle\tier2.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-autotile-tileset-prompts\tropical_jungle\tier3.md`

## Checks Run

- Searched the spec and prompt folder for limiting language such as `18-20`, `exactly 20`, `Create these 20`, `arrange the 20`, `5x4`, and `5 columns x 4`; no matches remained.
- Sampled the desert tier1 prompt.
- Sampled the updated autotile spec.

## Follow-Up Recommendation

- Generate the 16-tile core sheet first for visual/system validation, then add named expansion sheets for spoil overlays, transitions, hardpoint/socket interfaces, and trench-width variants as the renderer needs them.
