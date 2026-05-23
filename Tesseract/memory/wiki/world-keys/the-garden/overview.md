# The Garden

## Summary

The Garden is the public title for the farming/garden World Key. The active source prototype is still named Glassroot Garden / TWB-Farming internally.

## Scope

- Parent project: The World Beneath.
- World Key: The Garden.
- Internal/source name: Glassroot Garden.
- Code directory: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Prototype stack: Phaser 3.90, TypeScript, and Vite.
- Current scope: local browser prototype with local save-style persistence, a mix of approved PNG main-screen assets and remaining Phaser-drawn/prototype UI, plus UI-heavy farming/workbench loops.
- Not in current scope: Cloudflare/database integration, account sync, production persistence, final art, or platform reward authority.
- Current warning: the main-screen art pass still needs reference checks before replacing or deleting existing assets. See [[art-direction-and-asset-risks]] before broad Garden art or visual integration work.

## Current Prototype State

The prototype has a playable garden with 12 plots arranged as a 4x3 grid, Companion planting and harvesting automation, a storage/workbench overlay, raw and dried plant bins, a drying rack, Bundler recipes, Notice Board contracts, Transfer Bundles, finished bundle storage, compost heap, mastery XP, tier progression, and debug helpers.

The full-loop playtest gate has passed. The current Garden work is a clean asset-conversion restart from approved source sheets. The boundary geometry has stabilized around a back wall, tool nook, store entry, worker break entry, bottom boundary wall, side walls, `60px` centered corner caps, top wall returns, and top corner planters. Later updates locked in a `4 x 3` 12-plot layout, tier 1 plot art, grass ground tile, tier 1 well, tier 1 compost heap, the lantern-free store entry, utility-area cleanup, and door marker plaques.

The 2026-05-16 artifact pass explained the user-visible all-plots plant/bar issue as default-visible plot child objects when startup failed before `refreshAllPlots()`. Plot child objects are now created hidden and shown only by `refreshPlot()`. Later passes installed the starter-pet selector board with Chuck/Peggy/Stanly imagery, added layered worker-break portal and door sprites, tuned door holds/preopen timing, added inventory signposts, shaped plot outlines, compost fill overlay, well sparkles, plot-selection sparkle feedback, and slower companion movement. The worker-break path now uses separate looping portal-background and door-foreground sheets, companion depth sits above the doorway, and tier 2-5 plot/well/compost variants are wired from approved cutouts via `getUnlockedGardenTier()`. The most recent passes also wired all 5 well and compost tiers plus compost-fill mounds, generated a cyan-matte seed bag UI source set that still needs runtime wiring, completed direct drying-room click flow, and installed the 21 crop plant folders with 8 stage sprites each. `npm run build` passed through the latest reported pass.

The latest Garden passes made the seed bag image-backed from cleaned alpha crops, moved growing timers into the plot info panel, switched seed-stage markers to the real `seed-planted` sprite where available, tuned seed packet icon placement, kept drying-room occupied slots manually inspectable while drying, and made ready bundles manually collectable while the room is open. The starter-pet board is now the current selector direction and replaces the old circular selector. Chuck, Peggy, and Stanly are wired with icon images plus roaming/walk sprites.

Notice Board quest bundles are treated as one-off orders once queued or completed, while Transfer Bundles remain the repeatable route into shared storage. A 2026-05-17 hardening pass verified the Greenward Order lifecycle on a clean browser save through `Open`, `Awaiting completion`, and `Complete`; duplicate quest production stayed blocked while awaiting and completed; Transfer Bundles remained repeatable; and save/reload checks passed with no source changes.

The 2026-05-18 Herbalist Workbench / Storage Hut presentation pass moved the room toward approved image-backed assets: basement brick/floor backdrop, wooden work table, wall-mounted drying rack, ornate Notice Board, and image-backed raw/dried storage panels. Notice Board and Transfer Bundle recipe data now live in `src/data/bundleCatalog.ts`. The generated Notice Board catalog contains 100 orders per tier, 500 total, and orders now require exactly 3 distinct plant inputs with varied quantities. Notice Board cards show one-line titles while detailed requirements remain in the Bundler panel. Raw/dried bins are scrollable, capped at 999 units each, and no longer expose whole-bin compost controls.

The 2026-05-19 decommission report confirmed the mobile/touch review direction: portrait-phone Phaser Scale.FIT makes the Workbench too small, so the current direction is to require or support landscape instead of squeezing the room further. The same pass advanced Garden achievement UI/scaffolding, Garden pet board/roster/stamina/subskill scaffolding, platform pet catalog/account-owned pet fallbacks, and finished-bundles rack/package presentation.

Current gate: restart the bundling-machine art pipeline narrowly. The latest v6 runtime sheets were processed and wired, but visual QA failed because independently generated moving press/clamp pieces did not share stable anchors, sockets, or a single Phaser composition footprint. The next worker should inspect whether the failed v6 runtime path is still visible, hide/revert it if needed, then use SLYNYRD/external pixel-art references to design a stricter modular bundling-machine asset contract before more code or asset generation.

## Build And Test

Run from `C:\Users\yrred\Desktop\Unity\TWB-Farming`.

- Dev server: `npm run dev`
- Local test URL: `http://127.0.0.1:5173/`
- Required check after code changes: `npm run build`
- No dedicated lint or automated test suite is defined yet.

## Naming Rule

Use The Garden for public-facing release, marketing, and player-facing notes unless the user changes the naming decision. Use Glassroot Garden only when referring to internal/source history, code, or existing project files. The current approved layered source sheet is `C:\Users\yrred\Desktop\ChatGPT Image May 13, 2026, 07_31_20 PM.png`.

## Sources

- [[short-term/2026-05-12-glassroot-garden-working-window-intake]]
- [[short-term/2026-05-13-glassroot-garden-worker-final-decommission-report]]
- [[short-term/2026-05-13-glassroot-garden-asset-conversion-restart-report]]
- [[short-term/2026-05-16-garden-worker-final-decommission-report]]
- [[short-term/2026-05-16-glassroot-garden-visual-artifact-pet-selector-report]]
- [[short-term/2026-05-16-glassroot-garden-starter-pets-selector-wiring-report]]
- [[short-term/2026-05-16-glassroot-garden-worker-break-portal-door-layered-animation-report]]
- [[short-term/2026-05-16-glassroot-garden-tier-2-5-variant-wiring-report]]
- [[short-term/2026-05-16-glassroot-garden-tier-check-seed-bag-ui-report]]
- [[short-term/2026-05-16-glassroot-garden-drying-room-click-flow-report]]
- [[short-term/2026-05-16-glassroot-garden-herb-sprite-wiring-report]]
- [[short-term/2026-05-17-garden-worker-final-decommission-report]]
- [[short-term/2026-05-17-glassroot-garden-notice-board-lifecycle-hardening-report]]
- [[short-term/2026-05-18-glassroot-garden-worker-report]]
- [[short-term/2026-05-19-glassroot-garden-worker-final-decommission-report]]
- [[wiki/game-dev/project-hierarchy]]
- [[wiki/game-dev/world-keys]]
