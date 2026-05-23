# Full Loop Test And Implementation Plan

## Goal

Make the Glassroot Garden loop actually work end to end:

1. Plant crops from the Seed Bag.
2. Pets till, fetch seed, and plant.
3. Crops grow through visible stages.
4. Optional pet actions can improve or reduce yield.
5. Pets harvest crops.
6. Harvested raw herbs appear in raw bin crates.
7. Player drags raw herbs to the drying rack.
8. Herbs dry with timing based on crop tier.
9. Dried herbs appear in dried bin crates.
10. Player selects a Notice Board recipe or Transfer Bundle recipe.
11. Player drags dried herbs into the Bundler in recipe order.
12. Bundler creates a bundle with processing time based loosely on the recipe herbs.
13. Finished bundle appears in the finished bundle rack.
14. Finished bundle resolves automatically into:
    - selected contract completion, or
    - separate World Key shared storage.

World Key shared storage is explicitly separate from the main game inventory. Main-game pets can work in World Key games, but World Key bundle outputs do not become directly usable main-game items.

## Current Status

### Already Working Or Partly Working

- Seed Bag opens.
- Seeds can be dragged onto plots.
- Pets till soil, fetch seed, and plant.
- Crops grow on timers.
- Optional growth windows exist.
- Optional pet actions can succeed or fail.
- Yield changes based on optional work success/failure.
- Pets harvest ready crops.
- Harvests add raw materials to raw bin slots.
- Overflow goes to compost.
- Storage Hut / Herbalist Workbench view exists.
- Notice Board recipes exist visually.
- Transfer Bundle selection exists visually.
- Bundler panel displays the selected recipe.

### Not Yet Working

- Persistent Cloudflare account/database integration is still future work for this prototype branch.
- World Key shared storage is currently local prototype state, not server-authoritative storage.
- Notice Board contracts are static prototype recipes, not yet generated/rotated server-side.
- Automated regression is currently run as an ad hoc browser script, not yet checked in as a reusable test command.

## Implementation Steps

### Step 1: State Foundations And Timing Rules

Status: complete.

- Add crop tier and drying time metadata.
- Add drying rack slot state.
- Add bundler loaded-entry state.
- Add finished bundle slot state.
- Add contract/shared-storage destination state.
- Add World Key shared storage state separate from main-game inventory.
- Add helper functions for tier-based drying and recipe-based bundle processing time.

Acceptance:

- Build passes. Completed with `npm run build`.
- Existing farm loop is not intentionally changed by this step.
- Storage state is represented in code even if drag/drop is not yet wired.

### Step 2: Current Loop Browser Test

Status: complete.

- Open the game locally.
- Plant at least one quick crop.
- Catch one optional action window where possible.
- Let the crop harvest.
- Verify raw bin count changes.
- Verify no console errors.

Acceptance:

- Current implemented loop is verified.
- Seed Bag opens and seed selection queues Companion planting.
- Companion tilling, seed fetch, planting, growth, harvest, and lockdown reset were verified.
- Optional work/yield variation was verified: two Basil harvests paid base yield, and one clicked-window Basil harvest paid a higher yield.
- Raw Plant Bins showed 7 Basil after the test harvests.
- Browser console had no game errors. The missing favicon error was removed with an inline empty favicon.

Notes:

- Browser automation did not reliably trigger Phaser drag events on the seed packet, so a click-to-select seed fallback was added while preserving drag/drop behavior. This gives the game a better accessibility path and gives testing a stable input path.

### Step 3: Raw Herb Drag To Drying Rack

Status: complete.

- Make occupied raw bin slots draggable.
- Dropping onto the drying rack consumes raw herbs.
- Create active drying rack slot.
- Show herb hanging on the drying rack with timer.
- Use drying time based on crop tier.

Acceptance:

- Raw herb count decreases. Verified with Basil going from 2 raw to 1 raw, then 0 raw.
- Drying rack shows active herb and tier-based timer. Verified two Basil herbs hanging with independent timers.
- Drag/drop works from raw bin to drying rack.
- Click fallback also works: click raw herb, then click drying rack to hang one.

### Step 4: Drying Completion To Dried Bins

Status: complete.

- Resolve drying timers.
- Move completed herbs into dried bins.
- If dried bins cannot accept the item, leave the herb ready on the drying rack instead of destroying it.
- Refresh storage UI.

Acceptance:

- Dried herb count increases after timer. Verified with a browser test using Basil.
- Empty drying slot is freed after successful move.
- Rack timer displays `Ready` if a completed herb cannot move because dried bins are full.
- `npm run build` passes.

### Step 5: Dried Herb Drag Into Bundler

Status: complete.

- Make occupied dried bin slots draggable.
- Dropping into Bundler validates against selected recipe entry.
- Load order must match recipe order.
- Required amounts must match recipe amount.
- Visual load list shows locked entries.

Acceptance:

- Incorrect herb/order is rejected. Verified by selecting Mooncalm, attempting to load dried Basil, and confirming nothing loaded.
- Correct herb/order locks into Bundler. Verified by selecting Greenward and loading 1/4 dried Basil.
- Dried bin count decreases by one when a correct dried herb is loaded.
- Visual load list updates with loaded counts and locked rows.
- `npm run build` passes.

### Step 6: Bundle Creation And Processing Timer

Status: complete.

- Bundle button becomes active only when recipe is fully loaded.
- Dried herbs are consumed as they are loaded into the Bundler; the Bundle button consumes the loaded machine contents.
- Create finished bundle record.
- Place bundle into first empty finished-bundle slot.
- Processing time varies based on recipe herb drying times.

Acceptance:

- Finished bundle rack shows occupied basket and timer.
- Verified with a browser test: Greenward Order was loaded, bundled into finished rack slot 1, set to `processing`, and received a 2 minute processing timer.
- `npm run build` passes.

### Step 7: Contract And Shared Storage Resolution

Status: complete.

- Notice Board bundles auto-complete their selected contract when processing completes.
- Transfer bundles move to World Key shared storage when processing completes.
- World Key shared storage is a separate local namespace from the main game.
- Add visible count/status for shared storage.

Acceptance:

- Contract completion and transfer completion are visible.
- Shared storage output does not appear as main-game inventory.
- Verified with a browser test:
  - Greenward Order resolved into +18 Gardening Tokens and +9 Board XP.
  - Basil Transfer Bundle resolved into 1 Basil bundle in World Key shared storage.
  - Transfer bundle did not pay Notice Board tokens or Board XP.
  - Resolved bundles cleared out of the finished rack.
- `npm run build` passes.

### Step 8: Full Loop Regression Test

Status: complete.

- Plant, grow, optional action, harvest.
- Raw bin receives material.
- Raw herb dries.
- Dried herb enters dried bin.
- Recipe selected.
- Dried herbs loaded into Bundler.
- Bundle produced.
- Bundle resolves to contract or shared storage.
- Run build and browser smoke test.

Acceptance:

- The full loop works without console errors.
- Verified with a browser test:
  - Planted 3 Basil, 2 Sage, and 1 Yarrow through the Seed Bag and Companion automation.
  - Clicked an optional Tend / Charge window on Basil and verified it completed successfully.
  - Auto-harvest produced enough raw herbs for Greenward Order: 7 Basil, 4 Sage, 2 Yarrow.
  - Moved 4 Basil, 3 Sage, and 2 Yarrow from raw bins to the drying rack.
  - Drying timers completed and moved the recipe materials into dried bins.
  - Loaded dried herbs into the Bundler in recipe order.
  - Created Greenward Order in the finished rack with a 2 minute processing timer.
  - Resolved the bundle into +18 Gardening Tokens and +9 Board XP.
  - No browser console errors were reported.
- `npm run build` passes.
