# Garden Worker Final Decommission Report

## 1. Current Working Context

Project path:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming`

Project identity:

- Parent project: The World Beneath.
- World Key: The Garden.
- Source/prototype name: Glassroot Garden / TWB-Farming.
- Runtime: browser-native Phaser/Vite/TypeScript.

Active scene/code files:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\main.ts` remained the Phaser bootstrap and was not a primary edit target.
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\platform\twbPlatformClient.ts` existed as platform support; this decommission pass did not edit it.

Current task brief followed:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-glassroot-garden-task.md`
- Original immediate gate was to address the user-visible all-plots plant/blue-bar artifact before broad pet-selector work.
- Work later expanded by user direction into pet selector, pet sprites, door animation, garden interactability, plant sprites, seed bag UI, herbalist drying-room UI, bundling flow, and the Notice Board duplicate-order guard.

Dev server/build status:

- Latest `npm run build` passed on 2026-05-17 after the Notice Board duplicate-order guard.
- Local dev server at `http://127.0.0.1:5173/` returned HTTP `200` during this decommission pass.
- Dev server log artifacts are still present under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\`.

Current visual/artifact/pet-selector status:

- The earlier all-plots mature plant/blue-bar artifact was not reproduced in a clean Playwright context. It was not given a dedicated code fix because clean screenshots did not show it. It remains a user-browser/localStorage-save-state risk, not a clean-render reproducible bug.
- The old circular pet selector is no longer the intended current state. The installed pet selector is the wood/plaque board on the brick wall in the pink-square placement area, not over the door.
- Starter pet plaque currently shows Chuck, Peggy, and Stanly in framed khaki-backed openings without old rings or names.
- Starter pet moving sprites are wired into the roaming/work pets. Pet speed was slowed repeatedly, pet action tags were reduced, and action labels should show meaningful plot/action work rather than generic roaming.

## 2. What Changed

Primary code/system changes:

- Main Garden scene rendering was extended substantially in `GlassrootGardenScene.ts`.
- Pet selector board was installed, moved into wall space, resized/tuned, and wired to starter pets.
- Starter pets Chuck, Peggy, and Stanly now use icon images in the plaque and sprite sheets for moving garden pets.
- Pet movement was slowed several times and adjusted for door interactions.
- Door systems were added/tuned:
  - right-hand herbalist/storage hut door animation with interior.
  - middle tool-shed door animation with shallow cabinet/tools interior.
  - left worker-break/pet-shed door with two layered animations: separate portal loop behind separate door sheet.
  - pets are kept above door layers.
  - door-hold behavior was added so multiple pets do not reset a door animation; doors should stay open until the last pet leaves.
- Pet shed entry effects were added:
  - sparkle/pop particle burst.
  - twist/shrink disappearance.
  - portal door opens before pets emerge.
- Well sparkle particle effect was added.
- Water/compost labels were moved to signposts; water text removed and the numeric count is shown on the sign.
- Compost inventory was tuned to `99` capacity rather than `999`.
- Compost heap was moved/tuned to fit signpost placement.
- Compost heap fill visual was added using a compost mound overlay that fades/fills upward.
- Compost smell wisps were added/tuned in green/brown.
- Tier 2-5 plot, well, and compost variants were wired.
- Plot hover/active highlighting was changed from a square to a plot-shape outline using alpha/shape-based treatment.
- Seed bag UI was replaced with a themed generated UI set, then tuned with tier tabs and larger readable seed cards.
- Plant sprites were generated/cleaned and wired for all defined crop stages:
  - seed-planted.
  - sprout.
  - mature.
  - ready-harvest.
  - raw-bin.
  - drying-undried.
  - drying-dried.
  - dry-bundle.
- Plant placement on plots was moved upward/toward plot centers.
- Pets now carry seeds from the tool chest toward plots using a simple floating/telekinetic presentation.
- Seed bag closes once a seed is planted/committed.
- Plot timers were removed from top-of-plant overlays and moved into the plot info window.
- Plot info window was themed to match the Garden UI.
- Drying rack plants can be clicked/inspected for remaining time.
- Herb drying room was indexed and partially rebuilt from wireframe toward a themed room:
  - mobile-usable raw plant and dried herb storage card panels replaced small slot grids.
  - raw cards load to drying rack.
  - dried cards load to bundler/packing machine.
  - Notice Board/transfer bundle tabs exist.
  - finished bundle rack exists.
  - Bundler/packing machine remains mostly drawn/prototype, not a final layered asset implementation.
- Latest Notice Board bundle change:
  - Notice Board quest bundles now become `Awaiting completion` after being queued into the finished bundle rack.
  - Duplicate production of that same Notice Board quest bundle is blocked while awaiting completion.
  - Completed Notice Board orders are blocked from being produced again.
  - Transfer bundles remain repeatable.

Assets installed, removed, converted, or preserved:

- Installed/converted:
  - pet selector board asset.
  - starter pet icons and starter pet walk sheets.
  - herbalist/storage hut door sheet.
  - tool-shed door sheet.
  - worker-break/pet-shed portal loop sheet and door sheet.
  - inventory signpost assets.
  - tier 2-5 garden plot/well/compost variants.
  - compost fill mound overlays.
  - full plant sprite stage set for current crop list.
  - seed bag UI assets.
  - herbalist-room storage-card UI assets.
- Preserved:
  - raw/source/candidate assets under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\`.
  - screenshots and short-term reports as evidence.
- Removed:
  - No source assets were intentionally deleted during this final phase.

All-plots plant/blue-bar artifact status:

- Clean Playwright/browser checks did not reproduce the original all-12-plots mature-plant/blue-bar artifact.
- Most likely risk remains a live-browser/localStorage save-state mismatch or older dev-server/browser cache state.
- The issue was effectively ruled out for clean render context, not fully proven in the user's exact browser save state.

Pet selector board exact state:

- Board is installed in `src\assets\glassroot\garden\pet-selector-board.png`.
- Board is rendered in `GlassrootGardenScene.ts`.
- Board is placed on the brick wall area between left and middle doors, not over a door.
- It contains Chuck, Peggy, and Stanly icons framed in the plaque.
- Old ring styling and pet name labels were removed from the plaque display.
- Companion slot hit areas/home points were preserved or adjusted only as needed for the visible board and pet flow.

## 3. Current Garden State

What currently works:

- `npm run build` passes.
- Main Garden screen renders with the approved architecture/boundary path.
- 12 plots render in a 4 x 3 arrangement.
- Tiered plot, well, and compost assets are wired.
- Tool shed and herbalist hut plaques are visible.
- Pet selector board is installed and visible.
- Chuck, Peggy, and Stanly are wired as starter pets with moving sprite sheets.
- Pets perform garden actions, carry seeds, and interact with doors.
- Door animations exist for herbalist, tool shed, and pet/worker-break portal door.
- Well sparkle and compost fill/smell visuals exist.
- Plot hover/active outlines exist.
- Seed bag is tier-tabbed and uses themed seed-card UI.
- Plant sprites display for growth/harvest/bin/drying/bundle stages.
- Herbalist room supports raw-to-rack, dried-to-bundler, Notice Board orders, transfer bundle tab, finished bundle rack, and the new Notice Board duplicate-order guard.

What is partially working:

- Herbalist room is visually much improved but is still partly drawn/prototype. The packing/bundling machine is not yet a final layered animated asset system.
- Door timing has been tuned through screenshots and feedback, but not exhaustively stress-tested across long sessions with many simultaneous pet jobs.
- Mobile-usable storage cards are improved but still need actual mobile/touch playtest.
- Plant asset placement is tuned enough to show, but crop-by-crop visual polish may still need passes.
- Notice Board orders are one-off now; rotation/replenishment of new orders has not been designed.

What is broken, blocked, or unverified:

- The original user-browser all-plots plant/blue-bar artifact was not reproduced in clean Playwright and remains unverified against the user's exact live Chrome/localStorage state.
- No dedicated automated unit/integration test suite exists for game logic. Build and browser automation are the current checks.
- Vite build still reports a large chunk warning due to large asset/runtime bundle size.
- Some image assets are large; future optimization/code splitting is advisable before distribution.
- Save-state migration was not comprehensively tested across all previous save shapes after the many UI and progression additions.

Exact local run instructions:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Farming
npm install
npm run dev
```

Open:

```text
http://127.0.0.1:5173/
```

Build check:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Farming
npm run build
```

## 4. Tests/Checks Run

Build:

- `npm run build` passed repeatedly through the worker run.
- Latest confirmed pass was after the Notice Board duplicate-order guard on 2026-05-17.
- Build warning remains: Vite warns that some chunks exceed 500 kB after minification.

Dev server/browser checks:

- Local dev server checked at `http://127.0.0.1:5173/`; HTTP `200` during final decommission.
- Browser/Playwright checks were used throughout for visual screenshots and interaction verification.

Latest focused Playwright check:

- Opened `http://127.0.0.1:5173/`.
- Cleared local save for a clean test context.
- Filled bundler with `notice_greenward_bundle`.
- Queued Greenward Order once.
- Tried to queue Greenward Order again; duplicate was blocked and event text reported it was already awaiting completion.
- Filled and queued `transfer_basil` twice; transfer bundle duplication remained allowed.
- Screenshot kept:
  - `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\notice-bundle-awaiting-guard-1280x720.png`

Checks that could not be run and why:

- No dedicated lint/unit test command exists in `package.json`.
- No broad save-state compatibility suite exists.
- The user's exact live Chrome/localStorage state was not fully inspected; clean Playwright contexts and user-provided screenshots were the main evidence for visual checks.

## 5. Files Touched

Primary source:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`

Primary asset files and directories touched/installed during this worker window:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\pet-selector-board.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-chuck.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-peggy.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-stanly.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-chuck-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-peggy-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-stanly-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\herbalist-door-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\tool-shed-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\worker-break-portal-loop-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\worker-break-portal-door-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\inventory-sign-post.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\inventory-sign-post-short.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-5.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-5.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-5.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-5.png`

Bulk plant sprite files:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\seed-planted.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\sprout.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\mature.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\ready-harvest.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\raw-bin.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\drying-undried.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\drying-dried.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\{crop}\dry-bundle.png`

The `{crop}` set currently includes:

- `basil`
- `thyme`
- `yarrow`
- `sage`
- `nettle`
- `middenbloom`
- `mugwort`
- `lavender`
- `rosemary`
- `rue`
- `vervain`
- `wormwood`
- `angelica`
- `wolfsbane`
- `belladonna`
- `foxglove`
- `henbane`
- `elder`
- `mandrake`
- `mistletoe`
- `rowan`

Seed bag UI assets:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_bag_panel.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_bag_header_plaque.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_bag_footer_plaque.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\close_button_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\close_button_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\close_button_pressed.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\small_nav_button_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\small_nav_button_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\small_nav_button_pressed.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\small_nav_button_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\plant_selected_button_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\plant_selected_button_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\plant_selected_button_pressed.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\plant_selected_button_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\page_badge_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\page_badge_selected.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\page_badge_locked.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_token_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_token_selected.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_token_locked.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\horizontal_trim_1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\horizontal_trim_2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\horizontal_trim_3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\vertical_trim_1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\vertical_trim_2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_bag_slot_grid_backing.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_selected.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_locked.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_empty.png`

Herbalist room UI assets:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\storage_panel_raw.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\storage_panel_dried.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_pressed.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\plant_summary_card_disabled.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\card_action_chip.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\scroll_rail.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\herbalist-room\scroll_thumb.png`

Short-term reports created during this worker window include:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-visual-artifact-pet-selector-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-starter-pets-selector-wiring-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-pet-plaque-measured-fit-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-starter-pet-walk-sheets-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-herbalist-door-animation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-tool-shed-door-animation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-worker-break-portal-door-layered-animation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-tier-2-5-variant-wiring-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-herb-sprite-wiring-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-drying-room-click-flow-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-seed-bag-ui-wiring-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-plot-timer-drying-rack-info-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-herb-drying-room-asset-index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-herb-drying-room-measured-assets-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-layered-packing-machine-research-intake.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-mobile-storage-card-ui-intake.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-storage-card-lineup-pass-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-glassroot-garden-notice-bundle-awaiting-guard-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-garden-worker-final-decommission-report.md`

Key screenshot/log artifacts kept:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\notice-bundle-awaiting-guard-1280x720.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\herbalist-room-storage-cards-lineup-pass3-1280x720.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-vite-devserver-out.log`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-vite-devserver-err.log`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\dev-server-local-test.log`

## 6. Cleanup Performed

- No source files were deleted.
- No permanent Obsidian memory files were edited.
- Temporary screenshots/logs under `output\playwright` were kept intentionally as visual evidence and debugging breadcrumbs.
- Generated/cut source and candidate assets under `output\asset-conversion\garden-main-screen` were preserved, not cleaned, because they are evidence/source material for future asset work.
- `dist\` may have been updated by `npm run build`; this was not manually cleaned.

Leftover artifacts Bob should know about:

- Many screenshots remain under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\`.
- Dev server log files remain under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\`.
- Asset conversion outputs remain under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\`.

## 7. Risks

Likely regressions:

- `GlassrootGardenScene.ts` is very large and now contains many systems. Future edits can easily cause render-order, hit-area, or timing regressions.
- Door animation timing is sensitive. Do not assume it is final without watching multi-pet interactions.
- Pet pathing around doors and tools can regress if home points, door thresholds, or depth constants are changed.
- Quest-order duplicate guard intentionally treats Notice Board orders as one-off. If Bob wants repeating daily/rotating orders, that needs a new order lifecycle rather than removing the guard.

Browser/localStorage/save-state risks:

- The original plant/bar artifact may have been caused by old saved state or browser cache. Clean Playwright did not reproduce it.
- Existing local saves may contain queued bundles, old selected recipes, or old plot/crop states that behave differently than clean-state tests.
- Save migration is currently opportunistic; no formal migration suite exists.

Asset/render-order risks:

- Door sprites, door plaques, pets, portal layers, and interior sprites share close depth ordering. Do not assume a plaque/door/pet order is safe without screenshots.
- Pet sprites are intentionally high layer so they do not disappear behind door sprites.
- Several assets are large and inflate the Vite bundle.
- Plant sprites were bulk cleaned and wired; individual stage/crop polish is not guaranteed final.

Next worker must not assume:

- Do not assume the all-plots artifact is solved for the user's live browser state.
- Do not assume mobile usability is proven; card UI was designed for larger click targets but not real-device tested.
- Do not assume herbalist room assets are final; the room is still part wireframe/drawn UI.
- Do not assume the packing machine research has been fully implemented. It was documented and partially reflected in planning only.

## 8. Memory-Worthy Notes For Bob

- The Garden is a browser-native Phaser/Vite/TypeScript World Key, not the main Unity game.
- Active code path is `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.
- `npm run build` passes as of 2026-05-17.
- Pet selector board is installed and replaces the old circular selector as the current visual direction.
- Starter pets Chuck, Peggy, and Stanly are wired with icons and moving sprites.
- Notice Board quest bundles are now one-off: open -> awaiting completion -> complete. Transfer bundles remain repeatable.
- The all-plots mature plant/blue-bar artifact was not reproduced in clean Playwright; treat as a live-browser/save-state issue unless reproduced again.
- The layered animation research for future machinery should guide the packing machine: static body plus small rotating/sliding/particle/glow child layers, not a huge full-machine sprite sheet.
- Herbalist room should prioritize mobile-friendly cards and larger controls over tiny slot grids.

## 9. Do-Not-Promote Notes

- Do not promote exact tuning values for pet speeds, door delays, or plaque offsets as permanent design truth.
- Do not promote temporary screenshots as design decisions.
- Do not promote rejected prompt drafts or interim generated-sheet attempts.
- Do not promote the current bundler/packing machine drawing as final art direction.
- Do not promote the clean-context artifact result as proof the user's live browser can never show the artifact again.

## 10. Recommended Next Worker Brief

Recommended narrow recommissioning brief:

```text
You are the next Garden / Glassroot Garden worker under Bob/orchestrator.

Scope: The Garden World Key only, browser-native Phaser/Vite/TypeScript project at:
C:\Users\yrred\Desktop\Unity\TWB-Farming

Read first:
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\overview.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\systems.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-garden-worker-final-decommission-report.md
- C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts

Immediate next gate:
Run npm run build, open http://127.0.0.1:5173/, and verify the herbalist room current state. Focus on one bounded task only:
either (A) harden the Notice Board/finished bundle lifecycle with user-save testing, or
(B) replace the prototype bundler/packing machine with the layered static+small-animation approach documented in the packing-machine research intake.

Do not edit permanent Obsidian memory. Write only short-term reports.
Do not spawn subagents unless Bob/orchestrator explicitly directs it.
Do not broaden into new art or new systems until the chosen gate is verified.
```

End state:

- This worker is decommissioned.
- Permanent memory was not touched by this decommission pass.
