# Glassroot Garden Herb Drying Room Asset Index

## Task
Index the current herb drying / storage room wireframe and produce the total non-herb asset list needed before creating or installing new art.

## Scope
- Parent project: The World Beneath.
- World Key: The Garden.
- Internal/source name: Glassroot Garden.
- Code target inspected: `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.

This is an asset-planning pass only. No new art was generated and no runtime art was installed.

## Current Room State
The herb drying room is currently built almost entirely from Phaser graphics/text helpers:

- `createStorageRoomOverlay()`
- `drawStorageRoomBackdrop()`
- `drawStorageWorkbench()`
- `drawDryingRacks()`
- `drawNoticeBoard()`
- `drawRawPlantBins()`
- `drawSlottedPlantCrate()`
- `drawFinishedBundleShelves()`
- `drawFinishedBundleCrate()`
- `createStorageActionButton()`
- `createStorageRoomButton()`

The existing installed `src/assets/glassroot/garden/` folder does not currently contain dedicated drying-room backdrop, drying-rack, crate, bundler, notice-board, or finished-bundle UI art. Herb sprites themselves are already wired separately through the plant sprite assets and are excluded from this list.

## Recommended Asset Structure
Do not create one baked full-room image with all interactive controls included. Use:

1. One opaque room shell/backdrop asset.
2. Modular prop assets for rack, bins, notice board, bundler, and output crate.
3. Reusable UI state assets for buttons, tabs, cards, slots, and highlights.

This keeps hover states, selected states, dynamic counts, drying timers, recipes, and drag/drop targets easy to maintain.

## Total Asset List
Recommended total: **35 non-herb sprites/assets**, preferably packed into **7 source sheets** plus one full-room backdrop.

### 1. Room Shell
1. `herbalist-room-shell-1280x720.png`
   - Full opaque room backdrop: wall, floor perspective, side depth, bench body, drawers, lighting, and broad tabletop.
   - Should not include dynamic labels, recipe cards, herb sprites, or clickable module content.

### 2. Drying Rack Module
2. `drying-rack-wall-panel.png`
   - Wood backing / pegboard area for the rack.
3. `drying-rack-rail-frame.png`
   - Rail set, posts, hooks/pegs; no herbs.
4. `drying-rack-empty-hook.png`
   - Reusable empty hanging-point marker, if not baked into the rail frame.
5. `drying-rack-slot-hover.png`
   - Subtle slot hover/inspect highlight.
6. `drying-rack-slot-ready-highlight.png`
   - Ready-to-collect slot cue.

### 3. Notice Board Module
7. `notice-board-frame-cork.png`
   - Large cork board frame and cork surface.
8. `notice-board-decor-note-a.png`
   - Decorative pinned paper note, no readable text.
9. `notice-board-decor-note-b.png`
   - Second decorative paper note variant.
10. `notice-order-card-normal.png`
   - Dynamic recipe/order card background.
11. `notice-order-card-selected.png`
   - Selected recipe/order card background.
12. `notice-board-tab-normal.png`
   - Reusable board tab.
13. `notice-board-tab-active.png`
   - Active board tab.
14. `notice-board-scroll-button.png`
   - Small up/down scroll button base.

### 4. Raw / Dried Bin Module
15. `plant-bin-crate-raw.png`
   - Raw plant crate frame, empty 15-slot grid, title plate area.
16. `plant-bin-crate-dried.png`
   - Dried plant crate frame, empty 15-slot grid, title plate area.
17. `plant-bin-slot-empty.png`
   - Reusable empty cubby/slot inset if slots are not baked into crate frames.
18. `plant-bin-slot-selected.png`
   - Selected dried-bin slot outline/highlight.
19. `plant-bin-slot-hover.png`
   - Hover cue for raw/dried bin slots.
20. `plant-bin-compost-confirm-strip.png`
   - Small lower strip/backplate for Compost / Confirm / Cancel actions.

### 5. Bundler / Processing Module
21. `bundler-machine-body.png`
   - Main alchemical bundler machine body, table device, rings, posts, base.
22. `bundler-funnel-glass.png`
   - Funnel/drop target glass piece; can be animated/tinted in Phaser.
23. `bundler-liquid-orb.png`
   - Cyan/teal orb or fluid chamber accent, non-herb.
24. `bundler-info-panel.png`
   - Right-hand recipe/status panel background.
25. `bundler-ingredient-row-normal.png`
   - Ingredient row default state.
26. `bundler-ingredient-row-active.png`
   - Ingredient row currently requested.
27. `bundler-ingredient-row-complete.png`
   - Ingredient row loaded/complete.
28. `bundler-load-zone-highlight.png`
   - Drop-zone/hover glow for loading dried herbs.

### 6. Finished Bundle Output Module
29. `finished-bundle-crate.png`
   - Finished-output crate/shelf frame with 12-slot layout.
30. `finished-bundle-slot-empty.png`
   - Empty output tray/basket.
31. `finished-bundle-slot-processing.png`
   - Occupied/processing tray base, without herb bundle art.
32. `finished-bundle-slot-ready-glow.png`
   - Ready-to-claim highlight/glow.

### 7. Shared Storage UI Buttons
33. `storage-button-small-normal.png`
   - Generic small action button: Bundle, Compost, Confirm, Cancel, Up, Down.
34. `storage-button-small-hover.png`
   - Hover state for the same.
35. `storage-button-small-pressed.png`
   - Pressed state for the same.

Optional, if the current blue button should also become themed:

- `storage-back-button-normal.png`
- `storage-back-button-hover.png`
- `storage-back-button-pressed.png`

If those are included, the total rises from **35** to **38**.

## Excluded From This Asset Request
The following should not be recreated in this pass:

- Crop/herb sprites: `raw-bin`, `drying-undried`, `drying-dried`, `dry-bundle`, and growth sprites.
- Main garden exterior assets.
- Pets.
- Door animations.
- Seed bag art.
- Well, compost heap, plot, or signpost assets.

## Suggested Source Sheet Packaging
Use cyan-matte sprite sheets for modular cutouts. Do not ask the generator for transparency.

1. `herbalist-room-shell-01` - opaque full-frame room shell.
2. `herbalist-drying-rack-module-01` - rack panel, rails, empty hook, hover, ready highlight.
3. `herbalist-notice-board-module-01` - notice board, decorative notes, cards, tabs, scroll button.
4. `herbalist-plant-bin-module-01` - raw/dried crates, slot states, compost action strip.
5. `herbalist-bundler-module-01` - machine body, funnel, orb, info panel, ingredient rows, load highlight.
6. `herbalist-finished-bundle-module-01` - output crate and slot states.
7. `herbalist-storage-button-states-01` - small buttons and optional back button states.

## Screenshot Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herb-drying-room-current-wireframe-1280x720.png`

## Checks Run
- Read current Garden brief and required project scope files.
- Inspected current room renderer in `GlassrootGardenScene.ts`.
- Listed current installed Garden assets under `src/assets/glassroot/garden/`.
- Captured a clean current drying-room screenshot at 1280 x 720.

No build was run because no source code or runtime assets were changed.

## Cleanup Performed
No temporary scripts were written. The Playwright screenshot was intentionally kept as visual evidence.

## Risks
- If the whole room is generated as one baked image, dynamic/interactive states will become brittle.
- Baked text should be avoided. Phaser should continue rendering labels, counts, timers, recipe names, and button text.
- Modular cutouts need the normal two-step cyan cleanup: remove the exact cyan matte, then remove edge-connected off-cyan fringe tones.

## Memory-Worthy Notes
- The drying room currently has no dedicated raster art package for the room/modules.
- Recommended package is 35 non-herb sprites/assets, or 38 if the Back to Garden button gets custom themed states.
- The herb sprites themselves are already a separate plant-sprite concern and should not be included in this room-art pass.

## Do Not Promote To Memory
- Exact proposed filenames until the user approves the asset package structure.
- The current screenshot path unless needed as local implementation evidence.

## Next Recommended Gate
User/orchestrator should approve whether to produce:

1. the 35-asset core package only, or
2. the 38-asset package including themed Back to Garden button states.

After approval, create image-generation prompts sheet-by-sheet, then perform the cyan/off-cyan cutout pipeline before wiring assets into the room.
