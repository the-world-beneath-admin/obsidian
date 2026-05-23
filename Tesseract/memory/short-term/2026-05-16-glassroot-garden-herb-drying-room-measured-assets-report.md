# 2026-05-16 Glassroot Garden Herb Drying Room Measured Assets Report

## Task

Measure the current herb drying/storage room UI exactly, update the asset creation plan with the measured footprints, then create candidate assets for the room using sheet-based source where practical and the Garden cyan/off-cyan cleanup process.

Scope: Glassroot Garden World Key.

## Result

Completed a measured asset pass for the herb drying/storage room. The current UI was captured and measured from the existing Phaser scene, then a candidate asset package was created under the Garden output folder.

No runtime install was performed. These assets are candidates for visual review before wiring.

## Current Asset Measurements

Measurement plan:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\Herbalist_Drying_Room_Asset_Measurements_And_Creation_Plan.md`

Key measured footprints:

- Room shell: `1280 x 720`.
- Visible room frame: `x=20 y=22 w=1240 h=676`.
- Drying rack module: `x=100 y=86 w=590 h=254`.
- Drying rack slot centers: `x=178,281,384,487,590`; `y=158,218,278`.
- Notice board module: `x=700 y=86 w=500 h=254`.
- Notice cards: `w=426 h=34`, centered at `x=940`, `y=148,188,228,268`.
- Raw plant crate: `x=77 y=411 w=202 h=170`.
- Dried plant crate: `x=293 y=411 w=202 h=170`.
- Crate grid inner area: `x=crateX+13 y=crateY+35 w=176 h=122`.
- Bundler module: approx `x=535 y=367 w=456 h=230`.
- Finished bundle crate: `x=997 y=367 w=228 h=230`.
- Back button: `x=1048 y=637 w=152 h=34`.

## Assets Created

Candidate package:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-room-assets-01\`

Created:

- `herbalist-room-shell-source.png` - full opaque room shell candidate, `1280 x 720`.
- `herbalist-room-modules-source.png` - cyan-matte source sheet.
- `herbalist-room-modules-clean-cyan.png` - cleaned cyan-matte sheet.
- `herbalist-room-modules-clean-alpha.png` - transparent cleaned sheet.
- `herbalist-room-modules-preview.png` - review preview with dark background and magenta bounds.
- `herbalist-room-modules-manifest.json` - component sheet coordinates and runtime footprints.
- `herbalist-room-modules-cleanup-qc.json` - cleanup verification.
- `herbalist-room-assets-guide.md` - human-readable asset guide.
- `crops\` - 37 cyan-matte component crops.
- `crops-clean-alpha\` - 37 cleaned transparent component crops.

The 37 module components include rack panels, rack highlights, notice board pieces, notice cards, raw/dried crates, bin slots, bundler parts, finished bundle slots, and themed storage/back button states.

## Assets Converted Or Not Converted

Converted/generated locally:

- 1 full room shell candidate.
- 37 module crops from a cyan-matte source sheet.
- 37 transparent cleaned crops from those module crops.

Not converted:

- No herb plant sprites were regenerated.
- No runtime `src/assets/glassroot/garden/` install was performed.
- No scene code was changed.

## Screenshots And Visual Outputs

- Current room reference: `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herb-drying-room-current-wireframe-1280x720.png`
- Asset preview: `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-room-assets-01\herbalist-room-modules-preview.png`
- Full shell candidate: `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-room-assets-01\herbalist-room-shell-source.png`

## Checks Run

- Verified candidate package exists.
- Counted cleaned transparent crops: 37 PNG files.
- Checked cleanup QC for all module crops.
- Confirmed `remaining_near_cyan_opaque_pixels: 0` for all 37 cleaned transparent crops.

Build was not run because no runtime files were installed or changed.

## Cleanup Performed

No throwaway source files outside the allowed output package were left behind.

Known retained artifacts are intentional review artifacts:

- The measured plan.
- The asset package.
- The Playwright reference screenshot.
- This short-term report.

## Risks

- The full room shell candidate has a strong diagonal light beam in the upper-left. It may be too visually assertive and should be reviewed before install.
- The assets are locally generated candidates, not final approved art.
- The module assets are mechanically measured to current footprints, but their final look should be checked in-game before replacing the wireframe.
- Runtime wiring will need to preserve current click behavior for raw plants, dried plants, drying rack slots, bundler interactions, and the Back to Garden button.

## Memory-Worthy Notes

- The exact current drying-room UI footprints are now documented in a project-local plan.
- The rack, notice board, crate, bundler, and storage button assets should be installed as modular components rather than one baked room image.
- The Garden cyan cleanup process should include exact cyan removal, edge-connected off-cyan removal, and an internal near-cyan check/recolor pass.

## Do Not Promote To Memory

- Do not promote the generated candidate art as final approved art yet.
- Do not promote the diagonal light-beam shell as accepted style until visual approval.
- Do not promote runtime behavior changes, because no runtime install happened in this pass.

## Next Recommended Gate

Review `herbalist-room-modules-preview.png` and `herbalist-room-shell-source.png`. If approved, install the selected assets into `src\assets\glassroot\garden\`, wire the storage room scene to use them, run `npm run build`, and capture a 1280 x 720 in-game screenshot.
