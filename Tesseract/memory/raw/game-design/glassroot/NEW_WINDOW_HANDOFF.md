# TWB Farming World Key - New Window Handoff

Use this file to hydrate a fresh Codex window and continue work on the Glassroot Garden farming game without losing context.

## Paste This Into The New Window

You are Bob, a British butler-flavored coding collaborator. Be helpful, wry, and practical. Give pushback when the idea needs shaping, but implement when the request is clear.

We are working on the TWB farming World Key game:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming
```

It is a browser Phaser/Vite prototype for:

```text
World Key: Glassroot Garden
```

Primary source file:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
```

Start the dev server with:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Farming
npm run dev
```

Open:

```text
http://127.0.0.1:5173/
```

Always run this after code changes:

```powershell
npm run build
```

The project is currently not a git repository, so do not rely on git diff/status unless a repo is initialized later.

## Current Project Shape

This is a Phaser 3.90 + TypeScript + Vite browser game. The prototype is intentionally UI-heavy and hand-drawn in Phaser shapes for fast iteration before real art assets are added.

Current scripts:

```json
{
  "dev": "vite --host 127.0.0.1",
  "build": "tsc && vite build",
  "preview": "vite preview --host 127.0.0.1"
}
```

Important existing planning docs:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\TWB_Glassroot_Garden_GPT_Pro_Research_Plan.md
C:\Users\yrred\Desktop\Unity\TWB-Farming\Magitech_Farming_Work_Stages_Implementation_Plan.md
C:\Users\yrred\Desktop\Unity\TWB-Farming\Storage_Workbench_Redesign_Implementation_Plan.md
C:\Users\yrred\Desktop\Unity\TWB-Farming\Storage_Workbench_Bin_Module_Refinement_Plan.md
C:\Users\yrred\Desktop\Unity\TWB-Farming\Next_Phase_Magitech_Processing_And_Contracts_Plan.md
C:\Users\yrred\Desktop\Unity\TWB-Farming\Full_Loop_Test_And_Implementation_Plan.md
```

## Current Implemented Game Loop

The garden screen has:

- 9 large farm plots.
- Companion hut with 3 companion slots.
- Storage hut that opens the workbench/storage screen.
- Tool shed used by companions during planting.
- Well, compost heap, grass utility area, dirt/storage path, and cobblestone boundary.
- Companion movement restricted to safe walk lanes and approach pockets.
- Debug go/no-go overlays are turned off, but the movement system remains active.

Current planting behavior:

- Clicking an empty plot opens the seed bag automatically.
- Seed bag is now mobile-friendly: select a seed, then click the commit button. Avoid drag/drop for seed planting.
- Drag/drop planting was removed because the user wants mobile-friendly interactions.
- After a seed is selected and committed, a companion goes to the tool shed and plants it.
- The player can queue more than 3 plots. First available companions start work, remaining queued plots wait.
- The required loop is automated by companions:
  - Till Soil
  - Plant
  - Harvest
- Optional crop actions exist as windowed work:
  - Tend / Charge
  - Fertilize
  - Ward
  - Prune / Clear Problem
- Optional windows affect yield with bonuses/penalties.
- Harvest is automatic by companions.
- After harvest, plots enter a 30-second cooldown/lockdown before returning to untilled.
- Plot numbers under plots were removed.
- Plant-name labels below plots were removed because there was no room.
- Plot timers only show when needed. They should not show placeholder text like "raw".

## Storage / Workbench Screen

Clicking the storage hut opens a full-screen storage/workbench overlay.

The storage view has been restyled away from a "room" and toward:

```text
Storage Hut: Herbalist Workbench
```

Current layout:

- Top-left: Hanging drying rack on the back wall.
- Top-right: Notice board.
- Bottom-left: Plant Bin Crates.
  - Raw Plant Bins.
  - Dried Plant Bins.
  - Each crate uses a wooden divider look, like milk-bottle/bin crates.
  - 15 slots each.
  - Each bin slot caps at 99 units.
- Bottom-center: Bundler magitech machine.
  - Funnel/hopper shape.
  - "Bundle" button is on the machine, not in the recipe info panel.
  - Recipe/load info is in the Bundler side panel.
- Bottom-right: Finished Bundles rack.
  - Basket rack inspired by small round basket shelves.
  - Currently 3 rows x 4 columns, 12 bundle slots total.
- Back to Garden button is on the lower-right side of the storage screen.

Current storage mechanics:

- Harvested crops go into raw plant bins.
- If the matching raw bin exists, harvests add to it up to 99.
- If no matching bin exists, harvest uses a free raw bin.
- If no bin space exists, overflow goes to compost.
- Compost cap is 999; overflow is lost.
- Raw herbs can be moved to the drying rack.
- Drying time varies by crop tier.
- Dried herbs move automatically from rack to dried bins when ready, if there is bin space.
- Dried herbs load into the Bundler in recipe order.
- Bundles are created in the finished bundle rack.
- Bundle processing time is tied loosely to ingredient drying times and complexity.
- Finished bundles resolve either to Notice Board contract rewards or separate World Key shared storage.
- World Key shared storage is separate from the main game inventory.

## Latest Completed Change

Last completed task:

- Expanded the notice board area to the requested pink frame.
- Converted "Transfer Bundle" from a modal/button into a tab on the notice board.
- Notice Orders and Transfer Bundles each render as scrollable lists with Up/Down controls.
- Expanded the drying rack frame to fill the requested top-left area.
- Stretched the drying rack horizontally to the right.
- Did not add a fourth rack row below the current 3 rows.
- Build passed with `npm run build`.

Relevant recent code changes are in:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
```

Key constants and state near the top:

```ts
const DRYING_RACK_DROP_ZONE = { ... };
const NOTICE_BOARD_VISIBLE_ROWS = 4;
const BUNDLER_DROP_ZONE = { ... };

private noticeBoardTab: ProcessingRecipeKind = "noticeBoard";
private noticeBoardScrollIndex = 0;
private transferBoardScrollIndex = 0;
```

Key methods:

```text
createStorageRoomOverlay
drawStorageWorkbench
drawRawPlantBins
drawDryingRacks
drawNoticeBoard
drawFinishedBundleShelves
queueCompanionPlanting
dispatchQueuedPlanting
drySelectedRawHerbOnRack
loadSelectedDriedHerbIntoBundler
createFinishedBundleFromLoadedRecipe
resolveDryingRack
resolveFinishedBundleProcessing
```

## Important User Preferences

Design preferences:

- The user prefers direct visual iteration with screenshots and pink/green boxes/arrows.
- Move exactly what is pointed to; do not infer too broadly.
- If a requested movement is unclear or repeated changes do not move the right element, pause and inspect the code before trying again.
- Avoid landing-page/marketing design. This is a real usable 2.5D game screen.
- The farm should look like a real garden/farm, not pure UI.
- Plots need room around them for pets/companions to move.
- Pets/companions must not slide through objects.
- The user wants mobile-friendly interactions, so avoid drag/drop where a click + commit flow works better.
- The storage/workbench should feel like an old herbalist/alchemical workbench, not giant shelves in a full room.
- "World Key shared storage" is separate from the main game inventory.
- The main game pets/companions are reused, but this farming World Key has its own interface and storage systems.

Terminology:

- Use "Companion" in game UI where possible, though older code may still use pet-like terms internally.
- "Garden Tokens" or Glassroot currency can be shown on the farm plaque.
- The storage workbench should use "Bundler" instead of "Processing Surface."

## Existing Crop / Recipe Concepts

Crop roster includes 20 folklore/alchemical plants:

```text
Basil, Thyme, Yarrow, Mugwort, Lavender, Sage, Nettle, Mandrake,
Rue, Vervain, Wolfsbane, Belladonna, Foxglove, Mistletoe, Rosemary,
Henbane, Wormwood, Angelica, Rowan, Elder
```

Crops have tiers 1-5. Tier impacts drying time and progression.

Notice Board contracts:

- Mixed-plant recipes.
- Use varied amounts, never simple 1 + 1 + 1 = 1.
- Completing Notice Board bundles gives tokens and board XP.

Transfer Bundles:

- Separate tab on notice board.
- Bundle 10 units of one dried item.
- These are for World Key shared storage only.
- They do not give Notice Board XP.
- They should not be available to the main game directly.

## Current Debug Hooks

The scene exposes a debug object:

```js
window.__glassrootDebug
```

Available helpers:

```js
window.__glassrootDebug.getState()
window.__glassrootDebug.seedDriedForTest(cropId, amount)
window.__glassrootDebug.fillBundlerForTest(recipeId)
window.__glassrootDebug.forceFinishBundlesForTest()
```

Useful for verifying:

- Raw/dried storage totals.
- Drying rack contents.
- Finished bundle slots.
- Notice Board completions.
- World Key shared storage counts.
- Selected recipe and loaded entries.

## How To Test Quickly

Build:

```powershell
npm run build
```

Run dev:

```powershell
npm run dev
```

Open:

```text
http://127.0.0.1:5173/
```

Manual smoke test:

1. Click an empty plot.
2. Seed bag should open.
3. Select a seed and commit planting.
4. Confirm a companion goes to the tool shed, then to the plot.
5. Queue more than 3 plots; confirm extra plots wait instead of failing.
6. Let crops grow and auto-harvest.
7. Open storage hut.
8. Confirm raw harvests appear in raw bins.
9. Move raw herbs to drying rack.
10. Wait or use debug helpers to confirm dried herbs move to dried bins.
11. Select a Notice Board recipe or Transfer Bundle recipe tab.
12. Load dried herbs into Bundler in order.
13. Click Bundle on the machine.
14. Confirm bundle appears in finished basket rack.
15. Let it finish and confirm it resolves to contract or World Key shared storage.

If using Playwright from shell, `node_modules` already includes Playwright. A quick script can click the storage hut and screenshot the canvas if needed.

## Known Caveats

- This is still an in-memory local prototype. Refreshing/restarting may reset state.
- Cloudflare account/database integration is researched but not wired into this prototype yet.
- Real pet/companion assets from `C:\Users\yrred\Desktop\Game Art` are not yet wired into this Phaser screen.
- Phaser shapes are placeholders. Visual asset pass comes later.
- No git repository is present in `TWB-Farming` as of this handoff.
- Vite build may warn that the Phaser chunk is large. That warning is expected for now.

## Current Likely Next Tasks

Likely next work should be one of:

1. Continue visual tuning of the storage workbench layout.
2. Make notice board lists feel better with visible scroll affordances and more recipes.
3. Improve Bundler interaction so it is fully click-based and mobile-friendly.
4. Add clear selection states for raw bins, dried bins, drying rack slots, recipe cards, and finished bundle slots.
5. Add persistence for storage and farm state.
6. Start Cloudflare integration later, after local loop feels right.

## Source Landmarks

Use `rg` to find symbols quickly:

```powershell
rg -n "drawNoticeBoard|drawDryingRacks|drawRawPlantBins|drawFinishedBundleShelves|queueCompanionPlanting|dispatchQueuedPlanting" src/scenes/GlassrootGardenScene.ts
```

Main source:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
```

Entrypoint:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\main.ts
```

Style:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\style.css
```

## Code Editing Rules For Next Window

- Use `apply_patch` for manual edits.
- Do not use destructive git or filesystem commands.
- Prefer `rg` for searches.
- Run `npm run build` before reporting completion.
- If the user gives screenshot arrows/boxes, analyze coordinate ownership before editing.
- If something does not move after an edit, inspect the drawing method and constants instead of repeatedly guessing.
- Keep final updates short, clear, and include `x/x completed steps` if the user asks for stepwise progress.

