# 2026-05-16 Glassroot Garden Mobile Storage Cards Assets Report

## Task

Scope: Glassroot Garden World Key / The Garden.

Stop using the rejected not-clean herb room storage UI assets, regenerate the storage card UI on a cyan `#00FFFF` source background using the new sprite generator/cleaner workflow, run the cyan cleanup process, wire the cleaned assets into the herb drying room, and verify the mobile-friendly raw/dried storage card UI.

## Result

Complete for this pass.

The first generated UI attempt under `herbalist-room-assets-02` was treated as rejected evidence and replaced. A new `herbalist-room-assets-03` pass was created on flat cyan source sheets, processed through the three-sweep cyan cleaner, installed into the runtime UI asset folder, and verified in the herb room.

The raw plant bin and dried herb bin are no longer tiny slot grids. They now render as scrollable, clickable card summaries. Raw cards load eligible plants into the drying rack when space is available. Dried cards load eligible herbs into the bundler when the current recipe expects them.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\storage_panel_raw.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\storage_panel_dried.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_pressed.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\card_action_chip.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\scroll_rail.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\scroll_thumb.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\Herbalist_Drying_Room_Asset_Measurements_And_Creation_Plan.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\Herbalist_Drying_Room_Design_Master_Sheet.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-mobile-storage-card-ui-intake.md`

## Assets Converted

Converted and installed from:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-room-assets-03\`

Source cyan sheets:

- `source-cyan\herbalist-storage-panels-ui-source-cyan.png`
- `source-cyan\herbalist-plant-summary-cards-ui-source-cyan.png`
- `source-cyan\herbalist-card-action-chip-ui-source-cyan.png`
- `source-cyan\herbalist-scroll-rail-ui-source-cyan.png`
- `source-cyan\herbalist-scroll-thumb-ui-source-cyan.png`

Runtime cutouts were copied from the cleaned `cutouts\` folders into `src\assets\glassroot\garden\ui\herbalist-room\`.

Explicitly not converted: the rejected `herbalist-room-assets-02` pass was not reinstalled.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\herbalist-room-mobile-storage-cards-cleaned-1280x720.png`

## Checks Run

- `npm run build` in `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- Cleaner QA files report `Remaining cyan in sheet: 0` for the generated sheets.
- Runtime PNG scan found `cyan_family=0` and transparent corners for all nine installed herb room UI PNGs.
- Playwright clean-context visual check seeded raw and dried herbs, opened the herb room, and captured the 1280 x 720 screenshot.

## Cleanup Performed

No throwaway scripts were written. Inline Node/Python checks were used and left no script files behind.

Rejected asset evidence under `herbalist-room-assets-02` was preserved, not deleted.

## Risks

- This pass only replaces the raw/dried storage bin UI assets and card-list interaction. It does not complete the full herb drying room art refresh.
- The source contact sheet preview for `assets-03` is visually crowded, but the actual per-asset source sheets, transparent sheets, cutouts, and runtime files are clean.
- `C:\Users\yrred\Desktop\Unity\TWB-Farming` did not present as a git repository from this shell, so file inventory is based on the worked paths rather than `git diff`.

## Memory-Worthy Notes

- The cyan workflow should be the default for new Garden 2D cutout assets: generate on flat `#00FFFF`, preserve source sheets, run the cyan cleaner, inspect QA, then install runtime PNGs.
- The new cleaner skill’s three-sweep process is appropriate for Garden assets: exterior flood removal, cyan-family fringe cleanup, and interior cyan spot cleanup.
- Raw/dried storage is moving toward mobile-first card summaries rather than slot grids.

## Do Not Promote To Memory

- Rejected `assets-02` visual choices.
- Temporary Playwright seed data used only for screenshot verification.

## Next Recommended Gate

Review the 1280 x 720 screenshot in `output\playwright`, then decide whether to continue replacing the rest of the herb drying room wireframe panels with properly measured cyan-source assets.
