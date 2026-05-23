# Glassroot Garden Worker Report - 2026-05-18

## Scope
The Garden / Glassroot Garden.

## Summary
This working window focused on the Storage Hut / Herbalist Workbench presentation and Notice Board hardening after the finished-bundle lifecycle gate had already passed. The room was moved from mostly hand-drawn Phaser shapes toward user-approved image-backed background, rack, table, notice-board, and storage-bin assets. The Notice Board recipe catalog was split out of the scene, expanded, randomized, and then audited so notice orders use three distinct plants with varied quantities.

## Work Completed
- Booted and used the local dev server at `http://127.0.0.1:5173/`.
- Reworked the Herbalist Workbench background composition:
  - Installed a basement brick wall / stone floor backdrop.
  - Installed a large wooden work table asset so the table reads as standing in the room, with lower legs mostly off-screen.
  - Removed older wall/frame/placard pieces that conflicted with the new background direction.
  - Moved the title text to the top-left room edge and removed the old "Hanging Drying Rack" placard.
- Installed and tuned a new wall-mounted drying rack:
  - Cleaned cyan and near-cyan edge fringe from the approved rack sheet.
  - Wired the rack art into the room.
  - Adjusted hanging herb bundle scale/placement so drying plants sit on the rack without overtaking the rails.
- Rebuilt the Notice Board presentation:
  - Installed cleaned notice-board UI assets from the approved cyan-backed sheet.
  - Wired full board, contract cards, tab buttons, scroll buttons, pins/notes, selected/completed/disabled card states.
  - Centered contracts in the board area.
  - Shifted card title wording right 5px.
  - Stretched the board frame upward by 20px while keeping card content stable.
  - Moved Notice Orders / Transfer Bundles tabs 20px left.
  - Moved the Notice Board title text up 20px to recenter it in the raised frame.
- Split Notice Board and Transfer Bundle recipe data into `src/data/bundleCatalog.ts`:
  - Generated 100 notice orders per tier, 500 total.
  - Kept Notice Board active slots filled with 4 posted orders.
  - Expired notice orders are replaced after a randomized 1-3 minute refill delay.
  - Moved world-key transfer bundles out of the main scene recipe block into the side catalog.
  - Preserved Transfer Bundle repeatability and Notice Board one-off lifecycle behavior.
- Audited notice-order recipes:
  - Found the catalog formula could create repeated same-plant inputs, especially tier 1 because the crop step collided with the crop count.
  - Replaced the generator with deterministic three-plant combinations plus rotated/reversed ingredient order and varied tier-based quantity sequences.
  - Verified all 500 generated notice orders have exactly 3 ingredients, 3 distinct plants, and 3 distinct quantities.
  - Cleaned legacy notice-board recipes so each also has exactly 3 distinct plant inputs with varied quantities.
- Rebuilt raw/dried plant storage bins:
  - Installed image-backed raw and dried storage panels, card assets, action chips, and square scroll buttons.
  - Removed whole-bin compost controls.
  - Removed slot-limit semantics and set raw/dried bin caps to 999 units each.
  - Added scrollable card lists with tap/click buttons and wheel/drag support for mobile/touch direction.
  - Removed the unwanted blue/green scroll rail artifacts and fixed the stray line behind inactive scroll buttons.
  - Tuned button size and position, herb icon position, card spacing, and header title/counter placement.
  - Current header tags are horizontally centered and were last moved up 4px vertically for better fit.
- Adjusted Notice Board card text:
  - Cards now show a single-line title only, using larger text.
  - Removed per-card input text from the board list because inputs are visible in the Bundler panel.
  - Card titles are truncated to `T# Title` and no longer include ` - inputs`.
- Updated Bundler/recipe flow to work with catalog-driven notice orders and transfer bundles.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\data\bundleCatalog.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\card_action_chip.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\drying_rack_wall.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_scroll_down_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_scroll_down_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_scroll_up_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_scroll_up_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_pressed.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\scroll_rail.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\scroll_thumb.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\storage_panel_dried.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\storage_panel_raw.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\back_wall_underlay.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\back_wall_underlay_trimmed_01.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\basement_backdrop_01.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\bottom_drawer_band.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\counter_surface_underlay.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\module_contact_shadows.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\quiet_reserved_zone_plates.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\room_outer_frame.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\upper_workbench_frame.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\work_table_area_chatgpt_01.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\work_table_area_v2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\background-kit-01\work_table_area_v4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_brass_pushpin.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_brass_screw_coin.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_contract_completed.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_contract_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_contract_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_contract_selected.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_cork_panel.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_corner_plate.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_full_empty.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_header_plaque.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_note_blue_pin.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_note_green_pin.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_note_red_pin.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_red_wax_seal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_scroll_down_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_scroll_down_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_scroll_up_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_scroll_up_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_small_nail.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_tab_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_tab_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\notice-board-kit-01\notice_board_tab_selected.png`

## Checks Run
- `npm run build` after code changes; final run passed on 2026-05-17 with only the known Vite large chunk warning.
- Node audit script over `src/data/bundleCatalog.ts`: 500 generated notice orders, 0 failures; each order has exactly 3 inputs, 3 distinct plants, and 3 distinct quantities.
- Node audit script over legacy scene notice recipes: 6 legacy notice recipes, 0 failures.
- Multiple Playwright/Chromium visual screenshots at 1280 x 720 under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\`.
- Visual checks covered: background/table/rack composition, notice-board fit, notice-board card text, storage-bin card/button/icon fit, storage-bin header title/counter placement, and live populated bin/notice-board views.

## Current State
- Storage Hut / Herbalist Workbench now uses the basement backdrop, work table, wall-mounted drying rack, notice-board art, and storage-bin art.
- Notice Board displays 4 active notice orders from the catalog and maintains refill behavior after expiry.
- Notice Board generated orders now vary inputs properly and no longer collapse into one repeated plant.
- Notice Board order cards show one-line title text only; detailed requirements remain visible in the Bundler panel.
- Transfer Bundles remain repeatable and are sourced from `bundleCatalog.ts`.
- Raw and dried bins are scrollable, have 999 unit caps, and no longer expose whole-bin compost controls.
- Latest bin header label/counter placement is horizontally centered and moved up by 4px in the top plates.

## Risks / Fragile Areas
- `GlassrootGardenScene.ts` remains large and presentation-heavy. Future work should continue moving data/config out of the scene when practical.
- Save compatibility should be watched around notice-board order slots because posted order IDs are persisted. The legacy recipes still exist for compatibility, but catalog changes may affect any saves referencing generated order IDs if formulas are changed again.
- Tier 2 and tier 5 currently have only three crop types in their tier pools, so every notice order for those tiers necessarily uses the same three plants, though order and quantities now vary.
- The image-backed UI depends on many hand-trimmed PNGs. Avoid replacing or deleting installed assets without checking references.
- Playwright visual checks were manual screenshot checks, not automated pixel assertions.
- The Vite large chunk warning remains unchanged and is not yet addressed.

## Memory-Worthy Notes
- The Notice Board / finished bundle lifecycle hardening gate passed before this visual pass and was not repeated.
- Notice Board orders are one-off posted orders; Transfer Bundles remain repeatable.
- Notice Board and Transfer Bundle recipe definitions now live in `src/data/bundleCatalog.ts`.
- Generated Notice Board catalog contains 100 orders per tier, 500 total.
- Notice orders now require exactly 3 distinct plant inputs with varied quantities.
- Expired Notice Board orders refill after a randomized 1-3 minute delay.
- Raw/dried plant bins are scrollable and capped at 999 units each.
- Whole-bin compost controls were removed from raw/dried bins.
- Approved image-backed assets now define the Herbalist Workbench room direction: basement brick wall/floor, wooden work table, wall-mounted drying rack, ornate notice board, and image-backed plant storage panels.

## Do Not Promote
- Any rejected intermediate background/table art quality judgments beyond the final direction.
- Temporary measurement guesses and pixel nudges unless they are needed for future maintenance.
- Screenshot artifacts as durable design facts.
- Failed or superseded prompt drafts for image generation.
- The exact random orders visible in screenshots; they are transient.

## Cleanup Performed
- Temporary crop images made only for local visual inspection were removed.
- Screenshot artifacts remain under `output\playwright\` as useful visual evidence for this handoff.
- No source assets, user files, raw evidence, or reports were deleted.
- No files were staged, committed, reset, or broad-cleaned.

## Next Recommended Gate
Run a focused mobile/touch review of the Herbalist Workbench now that the room is image-backed and the raw/dried bins are scrollable. Specifically verify tap targets, storage-bin scrolling, notice-board selection, Bundler loading, and Back to Garden behavior at phone-sized viewports before more visual polish is layered on top.
