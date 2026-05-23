# TWB Trenchworks - Trench Overlay Cutout Prompt Pass

Date: 2026-05-19
Scope: TWB Trenchworks only

## What Changed

- Updated the trench prompt pack so trench sprites are specified as overlay/cutout art rather than rectangular terrain-print tiles.
- Added Garden-style cutout guidance to the biome masters and all sprite prompts:
  - flat `#00FFFF` cyan source matte for transparent runtime space
  - mostly cyan/transparent non-trench side/background areas
  - visible pixels limited to trench excavation, spoil lips, walls, shadow, detritus, sandbags, timber, revetment, duckboards/floor, and prepared pad/socket marks
  - clean `1-2 pixel` black/dark cutout-safe outline where trench material meets cyan
  - cyan-family fringe cleanup friendliness
- Preserved the `512x512` modular tile rule and the three-tier requirement.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\desert\_biome_master.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\temperate_forest\_biome_master.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-blueprint-sprite-sheet-prompts\tropical_jungle\_biome_master.md`
- All 78 sprite prompt markdowns under `trench-blueprint-sprite-sheet-prompts\{biome}\`

## Checks Run

- Confirmed 3 biome folders.
- Confirmed 26 sprite prompt markdowns per biome, excluding `_biome_master.md`.
- Confirmed every sprite prompt includes overlay/cutout, no rectangular terrain-print, `1-2 pixel`, cyan-family cleanup, mostly non-trench transparent/cyan, and base biome map wording.

## Risks

- Image generation may still include labels or full rectangular fills if a full markdown file is pasted without emphasizing the hardened prompt block. For best results, paste the biome master prompt plus the hardened prompt block, not the whole document metadata and QA checklist.

## Follow-Up Recommendation

- Retry the desert `tw_phase1_front_straight` prompt after this correction and reject any result that fills each 512x512 module with rectangular dirt instead of cyan cutout space.
