# TWB Trenchworks - Trench Prompt Pack Master Prompts

Date: 2026-05-19
Scope: TWB Trenchworks only

## What Changed

- Converted each biome `_biome_master.md` from a reference-sheet style brief into a text-only biome master prompt.
- Updated all 78 trench sprite prompt markdowns to reference `_biome_master.md` as pasted text context, not as an attached image, literal texture, scene, or layout.
- Verified prompt pack completeness after the update.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\desert\_biome_master.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\temperate_forest\_biome_master.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\tropical_jungle\_biome_master.md`
- All 78 sprite prompt markdowns under `trench-blueprint-sprite-sheet-prompts\{biome}\`

## Checks Run

- Confirmed 3 biome folders.
- Confirmed 26 sprite prompt markdowns per biome, excluding `_biome_master.md`.
- Confirmed each biome has one `_biome_master.md`.
- Confirmed all sprite prompts include required markers: pattern id, biome, footprint, three tiers, `512x512`, `#00FFFF`, forbidden content, hardened prompt block, and QA checklist.

## Risks

- The image generator may still overfit if the master prompt is pasted too many times into one large combined request. Best next step is a small vertical slice: one biome, one or two dominoes, then visual review.

## Follow-Up Recommendation

- Start with desert `tw_phase1_front_straight` and `tw_utility_line_vertical` because desert readability exposes trench silhouettes and cell joins clearly.
