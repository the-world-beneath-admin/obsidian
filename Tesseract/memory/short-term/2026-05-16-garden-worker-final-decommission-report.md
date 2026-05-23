# 2026-05-16 Garden Worker Final Decommission Report

## 1. Current Working Context

Project scope: **The Garden / Glassroot Garden World Key**, a browser-native Phaser/Vite/TypeScript subgame under The World Beneath.

Active project path:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming
```

Active scene/code file:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
```

Active Codex/window context: Garden worker window, continuing the Garden main-screen asset conversion pass. No git repository was detected when `git -C C:\Users\yrred\Desktop\Unity\TWB-Farming status --short` was attempted earlier; it returned `fatal: not a git repository`.

Last user goal before decommission: integrate and visually place the newly approved pet selector plaque source sheet, after finishing the small tool-shed and herbalist door plaques. The pet selector work was interrupted and then rolled back from the live game scene before this report.

Main systems/assets touched during this work:

- Main Garden screen rendering in `GlassrootGardenScene.ts`.
- Garden wall/architecture assets in `src\assets\glassroot\garden\`.
- Asset-conversion outputs under `output\asset-conversion\garden-main-screen\`.
- Playwright screenshot evidence under `output\playwright\`.
- Short-term Garden conversion report:
  `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-glassroot-garden-asset-conversion-restart-report.md`

## 2. What Changed

### Main Architecture And Boundary Work

The Garden main screen was converted from the older procedural/vector-like mockup toward approved PNG assets.

Implemented or adjusted in `GlassrootGardenScene.ts`:

- Main back wall asset render:
  - `main-back-wall.png`
  - Back wall constants currently include `MAIN_BACK_WALL_LEFT`, `MAIN_BACK_WALL_TOP`, `MAIN_BACK_WALL_WIDTH`, and `MAIN_BACK_WALL_HEIGHT`.
- Wall-built door/entrance PNGs:
  - `worker-break-entry.png`
  - `tool-nook-entry.png`
  - `store-entry.png`
- Boundary wall assets:
  - `brick-garden-wall-bottom.png`
  - `brick-garden-wall-side.png`
  - `brick-garden-wall-corner-left.png`
  - `brick-garden-wall-corner-right.png`
  - `brick-garden-wall-top-return.png`
- Boundary placement/sizing was iterated heavily with user visual steering.
- Current side wall settings include:
  - `BRICK_GARDEN_WALL_SIDE_DISPLAY_WIDTH = 20`
  - `BRICK_GARDEN_WALL_SIDE_BOTTOM_OVERHANG = -1`
  - `BRICK_GARDEN_WALL_SIDE_CROP_TOP = 42`
  - `BRICK_GARDEN_WALL_SIDE_Y_OFFSET = 5`
- Current corner cap settings include:
  - `BRICK_GARDEN_WALL_CORNER_DISPLAY_SIZE = 60`
  - `BRICK_GARDEN_WALL_CORNER_VISUAL_INSET = 18`
  - `BRICK_GARDEN_WALL_CORNER_VISUAL_RAISE = 17`
  - `BRICK_GARDEN_WALL_TOP_CORNER_VISUAL_DROP = 3`
- Top corner brick returns are drawn by `drawTopCornerWallReturns(left, right)`.
- Ground planters at the top corners are drawn by `drawTopCornerGroundPlanters(left, right)`.

Installed Garden architecture/boundary assets currently present:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\main-back-wall.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\worker-break-entry.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\tool-nook-entry.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\store-entry.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\brick-garden-wall-bottom.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\brick-garden-wall-side.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\brick-garden-wall-corner-left.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\brick-garden-wall-corner-right.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\brick-garden-wall-top-return.png
```

### Ground, Plot, Well, And Compost Work

Installed and wired:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ground-grass-tile.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-1.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-1.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-1.png
```

Current plot layout:

- 12 plots total.
- 4 columns x 3 rows.
- Tier 1 plot PNGs wired into the plot grid.
- Old procedural brick paths and old plot backing/dirt decorations were removed from the visible field so the layout can be rebuilt with better path assets later.

Current utility anchors:

- Tier 1 well is installed and rendered.
- Tier 1 compost heap is installed and rendered.
- Prior subtle mockup blotches around well/compost were cleaned from the visible utility area.

### Door Marker Plaques

Approved source crop used:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\cyan-outline-decoration-crops-01\crops\024-cutout.png
```

Installed plaque base:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-door-marker-plaque.png
```

Current code state:

- `GARDEN_DOOR_MARKER_PLAQUE_TEXTURE_KEY = "glassroot-garden-door-marker-plaque"`
- Plaque texture preloaded.
- `drawGardenDoorMarkerPlaques()` renders:
  - Tool shed plaque at `x 668, y 126`
  - Herbalist hut plaque at `x 1021, y 126`
- The old pet/worker plaque was intentionally removed because the user is replacing the pet selector with a new work-board style plaque.
- The two door plaques use the same Y coordinate to avoid uneven alignment.
- Glyphs are procedural Phaser graphics on top of the plaque PNG:
  - crossed-tool glyph for the tool shed.
  - leaf glyph for the herbalist hut.

### Pet Selector Plaque Attempt

Approved source sheet received from user:

```text
C:\Users\yrred\Downloads\ChatGPT Image May 15, 2026, 06_12_33 PM.png
```

Preserved source and crop output:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\pet-selector-plaque-01\source\pet-selector-work-board-sheet-01.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\pet-selector-plaque-01\crops\pet-selector-board-primary-candidate.png
```

What happened:

- The top board was selected as the best candidate because it has the clearest three-slot read.
- A cyan cleanup pass was run and the candidate was exported.
- A first integration attempt was started but interrupted before the render method was complete.
- That half-installed attempt caused the scene to stop before later rendering, which made the tool/herbalist plaques disappear.
- The half-installed pet-board code was removed from live scene usage.
- The accidentally installed live asset was deleted:
  `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\pet-selector-board.png`
- The preserved candidate remains under `output\asset-conversion\garden-main-screen\pet-selector-plaque-01\`.

### Prompt Package Created

Created a GPT Pro prompt for a pet selector board:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\prompts\gpt-pro-pet-selector-work-board-sheet-01.md
```

This prompt is a queue item, not a completed/installed game asset.

## 3. Current State

### Working

- `npm run build` passes after the rollback of the half-installed pet selector board.
- The main Garden scene renders in a clean Playwright browser context.
- Tool shed and herbalist hut door plaques are visible again after the rollback.
- The current Playwright verification screenshot after rollback is:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-plaques-restored-after-pet-board-abort.png
```

- The render path currently has `SHOW_WALK_DEBUG_OVERLAY = false`.
- The old pet selector is still the three circular slot markers near the worker break door.
- The pet selector board is not installed into the live scene.

### Partially Working

- Pet selector board source/crop exists but is only a candidate.
- The candidate crop still needs user visual review/possible hand cleanup before live installation.
- The candidate looked acceptable at a quick dark-background view, but faint cyan/edge concerns may remain and should be rechecked before installing.
- Top corner planters are installed and visible, but their exact long-term art direction is not final if the user later decides they clutter the corner.

### Broken / Rejected / Blocked

- The interrupted pet-board install is explicitly rolled back and should not be treated as completed.
- The user reported a recurring issue: large plant sprites/artifacts and blue bars appearing over all plots in their live browser window.
  - Confirmed fact: the user screenshot showed mature-looking plant graphics and bars on all 12 plots.
  - Confirmed fact: a clean Playwright screenshot after rollback did **not** show the same plant artifacts.
  - Not investigated due to the decommission instruction.
  - The next worker must inspect this before resuming feature work.
- Path art is not currently rebuilt. The old bad dirt path attempt was rejected.
- The pet selector board remains blocked on a clean deliberate integration pass.

## 4. Tests And Checks Run

Primary build command used repeatedly:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Farming
npm run build
```

Result:

- Passed repeatedly during the session.
- Final run after rolling back the pet selector board passed.
- Expected Vite warning remains:
  chunks larger than 500 kB after minification.

Representative final build output:

```text
> twb-glassroot-garden@0.1.0 build
> tsc && vite build

✓ built
(!) Some chunks are larger than 500 kB after minification.
```

Browser/dev-server status:

- The local dev server was reachable at:

```text
http://127.0.0.1:5173/
```

- `Invoke-WebRequest -Uri 'http://127.0.0.1:5173/' -UseBasicParsing -TimeoutSec 5` returned status `200` during plaque verification.
- Node dev-server processes were observed running earlier.

Representative screenshot commands run:

```powershell
npx playwright screenshot --viewport-size=1280,720 --wait-for-timeout=3000 http://127.0.0.1:5173/ C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-plaques-restored-after-pet-board-abort.png
```

Important screenshot evidence produced:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-12-plot-layout-4-wide-3-tall.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-tier1-well-compost-installed.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-store-entry-lantern-removed.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-utility-mockup-blobs-removed.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-top-corner-wall-returns-05.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-side-walls-down-5.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-top-corner-ground-planters-02.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-marker-plaques-05.png
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-door-plaques-restored-after-pet-board-abort.png
```

Checks not run:

- No automated gameplay tests exist for this scene.
- No lint command was run or found as required workflow.
- The user-reported plant artifact issue was not investigated because decommission instruction stopped active work.

## 5. Asset Status

### Approved Source PNGs Used

Approved/user-provided or user-cleaned assets used in the live game include:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\candidates\...
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\cyan-outline-decoration-crops-01\crops\024-cutout.png
C:\Users\yrred\Downloads\ChatGPT Image May 15, 2026, 08_30_35 AM.png
C:\Users\yrred\Downloads\ChatGPT Image May 15, 2026, 06_12_33 PM.png
```

Note: The May 15 06:12:33 PM pet selector sheet is approved as a source sheet/candidate source, but it is **not installed into the live game** at decommission.

### Assets Installed Into The Game

Current installed Garden PNGs in `src\assets\glassroot\garden\`:

```text
brick-garden-wall-bottom.png
brick-garden-wall-corner-left.png
brick-garden-wall-corner-right.png
brick-garden-wall-side.png
brick-garden-wall-top-return.png
garden-compost-tier-1.png
garden-door-marker-plaque.png
garden-plot-tier-1.png
garden-top-corner-brick-left.png
garden-top-corner-brick-right.png
garden-top-corner-plant-left.png
garden-top-corner-plant-right.png
garden-well-tier-1.png
ground-dirt-tile.png
ground-grass-tile.png
ground-packed-earth-tile.png
main-back-wall.png
path-brick-tile.png
store-entry.png
tool-nook-entry.png
worker-break-entry.png
```

Important nuance:

- `garden-top-corner-brick-left.png` and `garden-top-corner-brick-right.png` still exist in `src\assets`, but the current active corner-return solution uses `brick-garden-wall-top-return.png`. The next worker should confirm whether the older top-corner brick files are still referenced before deleting anything.
- `pet-selector-board.png` is **not** present in `src\assets` after cleanup.

### Generated But Not Approved / Not Installed

Pet selector crop candidate:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\pet-selector-plaque-01\crops\pet-selector-board-primary-candidate.png
```

This is a candidate only. Do not install until reviewed.

### Rejected Or Suspect Asset Directions

Earlier rejected/suspect directions from this Garden restart remain relevant:

- The old isolated tool-nook/shed iteration was considered suspect when generated separately from wall context.
- Transitional architecture cluster sheets were not final production assets.
- Cobblestone fence direction was rejected/superseded by brick boundary walls.
- A standalone dirt-path asset attempt was visually rejected as too large/mismatched for the desired pathing.

### Cleanup Standard Used

Durable asset-pipeline lesson:

- Cyan matte + black outline worked much better for cutouts than magenta/fake transparency.
- Current cutout standard:
  - Solid cyan background.
  - Strong black outline.
  - Remove cyan-family pixels, including darker cyan edge shades caused by antialiasing.
  - QA on dark and light backgrounds before installing into `src\assets`.

## 6. Risks

### Current Technical Risks

- `GlassrootGardenScene.ts` is a large monolithic scene file. Small render-order mistakes can break unrelated visible layers.
- The door plaques are drawn after `createCompanionArea()`. If `createCompanionArea()` throws, the plaques will not render. This exact failure occurred during the interrupted pet-board attempt.
- Many art placements are hard-coded coordinates. Visual drift is easy if one wall/field constant changes.
- The scene uses local browser save/persistence; a clean Playwright context may not reproduce user-browser artifacts.

### Current Visual Risks

- Pet selector board candidate may still have faint cyan/edge artifacts and needs proper review before live install.
- The user-reported plot plant artifacts may be caused by saved plot state, crop rendering scale/layering, or another rendering issue. This is not confirmed.
- Door marker plaques are aligned at same Y coordinate, but final visual acceptance is still user-dependent.
- Top corner planters are installed; if future pathing/wall decoration changes, they may need to move again.

### Regression Risks

- Any new pet selector integration must avoid calling incomplete methods before a build/check.
- Any changes to companion slot rendering may affect:
  - companion selection hit areas,
  - selected slot highlight,
  - companion home points,
  - pet movement/task automation.
- Any cleanup/deletion of assets should first check code references with `rg`.

## 7. Memory-Worthy Notes For Bob

Durable facts:

- The Garden main screen currently has a working Phaser scene with approved PNG architecture, 12 tier-1 plots, tier-1 well, tier-1 compost heap, and door plaques.
- The active Garden project path is:
  `C:\Users\yrred\Desktop\Unity\TWB-Farming`
- The main scene remains:
  `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- The asset conversion process is now most successful when source art uses a solid cyan background plus a black outline.
- The pet selector board source sheet exists and is preserved, but no pet selector board is currently live.
- The current door marker plaque locations are:
  - Tool shed: `x 668, y 126`
  - Herbalist hut: `x 1021, y 126`
- The current path/debug overlay is off:
  `SHOW_WALK_DEBUG_OVERLAY = false`

Decisions:

- Do not keep trying to build Garden art from weak isolated assets.
- Install only user-approved source PNGs.
- Preserve source sheets and candidate crops under `output\asset-conversion\garden-main-screen\` before installing into `src\assets`.
- Pet selector board should replace the old circular pet selector, but should be integrated in a clean dedicated pass.

Warnings:

- Do not trust clean Playwright screenshots alone for persistence-related visual issues; the user's Chrome/localStorage state may show bugs that a clean context does not.
- Do not delete `src\assets` files without first checking `GlassrootGardenScene.ts` references.
- Do not resume the pet board from the half-installed attempt. Start fresh from the preserved candidate/source.

Open questions:

- What exactly caused the user-visible plant artifacts and blue bars on all plots?
- Is that artifact tied to saved crop state, plot rendering, Phaser depth/layering, or an incomplete previous task?
- Should the pet selector board be the top source-sheet board, or should the user choose another board variant from the source image?
- Should the pet selector board replace only visual circles, or also launch a real shared-inventory pet-swap modal now?

Next recommended gate:

- Before any new art integration, reproduce or explain the plant-artifact issue in the user's current save/browser state.
- Then perform a narrow pet selector board integration pass.

## 8. Do-Not-Promote Notes

Do not promote these as durable memory:

- Exact tiny coordinate nudges from every intermediate wall/corner attempt.
- Rejected old dirt path render.
- The interrupted pet-board implementation approach.
- Temporary guesses about the plant artifacts until inspected.
- Prompt drafts that were superseded by user-approved source images.
- Black screenshots from a Playwright capture glitch.
- Chat frustration, repeated steering, or transient visual complaints except as warnings about process risk.

## 9. Recommended Next Worker Brief

Recommended next task:

```text
Hydrate a fresh Garden worker for a narrow visual bug and pet selector stabilization pass.
```

Read first:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-glassroot-garden-asset-conversion-restart-report.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-garden-worker-final-decommission-report.md
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
```

Allowed write areas:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\
C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\
```

Forbidden / caution paths:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md
```

Done criteria for next worker:

1. Confirm current Garden scene builds with `npm run build`.
2. Reproduce or rule out the user-visible plot plant artifacts using the user's browser/save state if possible.
3. Do not install the pet selector board until the artifact issue is understood or explicitly deferred.
4. If installing the pet selector board:
   - Start from `pet-selector-plaque-01` source/crop.
   - Recheck edge cleanup.
   - Install into `src\assets` only after visual acceptance.
   - Add the render method before adding any call site.
   - Keep tool/herbalist plaques visible.
   - Run `npm run build`.
   - Capture a 1280 x 720 screenshot.
5. Write a short-term worker report.

Special cautions:

- The user's browser may contain local save state that Playwright does not share.
- Avoid one giant visual change. Use one chunk at a time.
- Do not resume from partial interrupted code; inspect current code first.

## 10. Cleanup Performed

Cleanup performed:

- Removed the accidentally installed live pet selector asset:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\pet-selector-board.png
```

- Removed the half-installed live pet selector references from `GlassrootGardenScene.ts`.
- Preserved the approved pet selector source sheet and candidate crop under `output\asset-conversion\garden-main-screen\pet-selector-plaque-01\`.

Cleanup not performed:

- Did not delete old screenshot evidence.
- Did not delete approved source sheets.
- Did not delete candidate crops.
- Did not delete any other installed Garden assets.
- Did not update permanent Obsidian memory.

