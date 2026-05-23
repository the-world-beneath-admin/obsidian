# TWB Trenchworks War Multi-Tile Cover And Concealment Report

Date: 2026-05-16
Worker: TWB Trenchworks playtest/asset worker
Scope: TWB Trenchworks standalone Unity 2D, war-side assets only.

## What Changed

- Added the first pass of larger multi-tile battlefield assets for war-side cover, concealment, slow terrain, and mixed tactical decoration.
- Updated the war asset style guide so any map decoration larger than `1x1` must have a gameplay role rather than being pure clutter.
- Created a multi-tile cover/concealment asset plan with footprints, roles, and intended gameplay tags.
- Generated two cyan-matte source sheets, removed the cyan matte, and cut the assets into transparent PNGs sized to their gameplay footprints.
- Created labelled review key images for visual inspection before Unity wiring.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-master-style-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-multitile-cover-concealment-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-output-index-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-large-cover-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-large-concealment-v1-key.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Source\war-large-cover-v1-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Source\war-large-concealment-v1-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Transparent\war-large-cover-v1-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Transparent\war-large-concealment-v1-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Normalized64\war-large-cover-v1-footprint-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Sheets\Normalized64\war-large-concealment-v1-footprint-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\MultiTile\war-large-cover-v1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\MultiTile\war-large-concealment-v1\`

## Asset Counts

- `war-large-cover-v1`: 16 cutouts.
- `war-large-concealment-v1`: 12 cutouts.
- Total multi-tile cutouts: 28.

Footprints used:

- `3x1`: `192x64`
- `2x2`: `128x128`
- `3x2`: `192x128`
- `3x3`: `192x192`

## Tests And Checks Run

- Validated 28 multi-tile cutout PNGs.
- Confirmed `0` validation issues.
- Confirmed each cutout matched its filename footprint.
- Confirmed no disallowed opaque cyan matte remained in the validated multi-tile cutouts.
- Confirmed key images were created for review.

## Cleanup Performed

- Removed small disconnected cyan/noise fragments from the generated multi-tile cutouts.
- Cleanup pass affected 13 files, removing 976 stray pixels across 162 detected disconnected components.
- Original generated image files under `.codex\generated_images` were preserved as raw generation evidence.

## Risks

- These are first-pass generated assets and should be visually reviewed before being wired into terrain generation.
- Rectangular gameplay footprints are ready now; later pathing may want more precise submasks for assets with irregular shapes.
- A few assets intentionally include small detached details such as net supports, brush fragments, or tangle scraps. If these read as noise in Unity, they should be simplified.
- Unity import settings and runtime terrain placement were not changed in this pass.

## Memory-Worthy Notes

- War-side decoration policy is now: any asset larger than `1x1` must be tactically meaningful as cover, concealment, slow terrain, blocking terrain, or a mixed terrain role.
- The current visual direction keeps war-side assets dark, grim, grid-readable, and black-outlined, while leaving production-side assets for a later, lighter visual pass.
- Multi-tile battlefield props should support the AI goal of moving from cover to cover instead of merely dressing the map.

## Follow-Up Recommendations

- Review `war-large-cover-v1-key.png` and `war-large-concealment-v1-key.png` in the docs folder and reject or revise any assets that do not read clearly at Unity zoom.
- Add Unity import settings for point filtering, no compression, transparent sprites, and correct pixels-per-unit once the exact sprite pipeline is final.
- Wire these assets into the random map prop system with gameplay tags for `cover_half`, `cover_full`, `concealment_half`, `concealment_full`, `movement_slow`, and `movement_blocking`.
- Add a debug overlay or tooltip key so the player can tell which props are cover, concealment, or movement hazards during playtests.

## Blocked

- No blocker for this asset pass.
- Runtime use is intentionally not wired yet; this pass prepared the assets and documentation for review first.

