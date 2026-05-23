# TWB Trenchworks - Raw Module Prompt Hardening

Date: 2026-05-19
Scope: TWB Trenchworks only

## What Changed

- Hardened the trench sprite prompt pack after the generated desert test produced a labelled presentation sheet and prebuilt trench strips.
- Updated prompt language so the primary output is raw `512x512` square trench overlay modules only.
- Clarified that each occupied local cell must become one directly cuttable/placeable runtime module.
- Clarified that the Unity renderer/map builder assembles dominoes by local cell coordinates.
- Forbid assembled strips, full domino paintings, labels, captions, arrows, cell numbers, border boxes, white boxed presentation layouts, and sheet decorations.
- Preserved overlay/cutout, cyan matte, `1-2 pixel` black/dark outline, biome styling, and tier progression rules.

## Files Touched

- All 78 sprite prompt markdowns under:
  `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\{biome}\`
- 3 biome master prompts:
  - `desert\_biome_master.md`
  - `temperate_forest\_biome_master.md`
  - `tropical_jungle\_biome_master.md`

## Checks Run

- Sampled `desert\tw_phase1_front_straight.md`.
- Sampled `desert\_biome_master.md`.
- Confirmed prompt language now emphasizes raw runtime modules, local-cell order, no assembled strips, and no presentation layout.

## Risk

- The image generator may still try to add labels if asked for too many tiers/cells at once. Best next generation test should request one small raw module sheet and explicitly forbid all text in the image.

## Follow-Up Recommendation

- Retry desert `tw_phase1_front_straight` using only the biome master prompt plus the hardened prompt block. If it still creates labels, make an even smaller test prompt for only tier1 modules first.
