# The Garden Art Direction And Asset Risks

## Status

Active warning - created 2026-05-13 after Garden worker decommission.

## Current Situation

The Garden main screen is in an active layered-source-sheet conversion. The restart now uses approved/source-reviewed PNG chunks rather than the earlier suspect cluster atlas. The current installed path includes the back wall, tool nook entry, store entry, worker break entry, bottom boundary wall, side walls, `60px` centered corner caps, top wall returns, top corner planters, tier 1-5 plot/well/compost visuals, door marker plaques, starter-pet selector board, layered worker-break portal/door sprites, signpost counters, plot outline asset, compost fill overlay, well sparkle particles, and image-backed Herbalist Workbench / Storage Hut room assets.

The Herbalist Workbench / Storage Hut direction now includes a basement brick/floor backdrop, wooden work table, wall-mounted drying rack, ornate Notice Board, and image-backed raw/dried storage panels. Remaining work is landscape-first mobile/touch review and tuning before broad new art installation.

The 2026-05-19 bundling-machine v6 pass failed visually: the moving press/clamp reads as detached and the generated parts do not share a stable compositional anchor. Treat that runtime path as evidence only until a modular replacement is designed.

## Rejected Or Do-Not-Use Assets

- Earlier isolated `tool-nook-entry.png` direction - rejected after the user said it read as mismatched generated art rather than a wall-built brick tool alcove. Do not treat the filename alone as rejected: the 2026-05-16 decommission report says a current `tool-nook-entry.png` is installed as part of the approved wall/architecture path. Check the actual asset and code references before changing or deleting it.
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-architecture-cluster.png` - rejected and deleted after the user rejected the transitional atlas build.
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\cobblestone-fence-u.png` - superseded direction; the user prefers brick boundary walls and corner pillars over the cobblestone fence attempt.
- Generated images under `C:\Users\yrred\.codex\generated_images\` from the 2026-05-13 Garden art session are unapproved unless individually inspected and accepted.
- The interrupted pet selector board install is rejected as an implementation path. The installed selector board is a later clean wiring pass and is the current baseline.
- The failed bundling-machine v6 runtime layout and detached moving press/clamp output are not a reusable pattern. Keep them only as evidence.
- Superseded - The user-visible all-plots plant/bar artifact was previously unresolved. It is now explained as default-visible plot child objects when startup failed before `refreshAllPlots()`, and the objects are now created hidden by default.

## Active Code Risk

`C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts` currently references the approved layered Garden install path and should continue to avoid reintroducing the rejected atlas:

- `main-back-wall.png`
- `tool-nook-entry.png`
- `store-entry.png`
- `worker-break-entry.png`
- `brick-garden-wall-bottom.png`
- `brick-garden-wall-side.png`
- `brick-garden-wall-corner-left.png`
- `brick-garden-wall-corner-right.png`
- `brick-garden-wall-top-return.png`
- `garden-plot-tier-1.png`
- `ground-grass-tile.png`
- `garden-well-tier-1.png`
- `garden-compost-tier-1.png`
- `garden-door-marker-plaque.png`

The door marker plaques are currently reported at:

- Tool shed: `x 668, y 126`
- Herbalist hut: `x 1021, y 126`

`SHOW_WALK_DEBUG_OVERLAY = false` is the current reported state.

## Accepted Direction

- Use `Garden_Main_Screen_Art_Master.md` as the master specification source rather than treating a single master PNG as the source of truth.
- Future art should be generated as coherent, high-resolution PNG chunks or sheets from explicit prompts and approved reference material.
- The target style is high-detail hand-painted cartoony, daytime big-city backyard garden, slight noir/cyberpunk mood, and about 30 percent old-world herbalist shop.
- Tool shed direction: a brick alcove built into the wall, with side returns and an overhang, not a freestanding shed or sticker-like object.
- The user prefers preparing a drop-in package for the ChatGPT website image generator because the user has GPT Pro; OpenAI API image generation would use API credits.
- Decoration extraction standard: flat cyan source background, deliberate black external outline, exact and near-exact cyan removal, edge-connected cyan-family cleanup including darker teal blur, contour-only cleanup of cyan-adjacent edge tones, then dark-background and light-background QA contact sheets before any install.
- Next Garden art sheet should move to ground/progression pieces rather than another wall-decoration sheet: grass and ground base pieces, modular paths, garden plot tiers, compost heap tiers, well tiers, and seam-hiding support pieces.
- Plot, compost, and well upgrade tiers should share footprints and anchors so art can swap without moving hit areas.
- Pet selector board source/candidate exists under `output\asset-conversion\garden-main-screen\pet-selector-plaque-01\`; the installed board should be tuned from the current baseline rather than reinstalled from the old interrupted path.
- Next bundler art gate: research Slynyrd/pixel-art animation and modular composition principles before any new prompt or code integration.

## Immediate Gate

Current immediate gate: review the image-backed Herbalist Workbench / Storage Hut at mobile/touch-sized viewports before adding more visual polish.

Continue the clean asset-conversion restart by keeping approved/user-reviewed source PNGs as the only active install path:

- treat `garden-architecture-cluster.png`, the rejected isolated tool-nook direction, cobblestone fence attempts, and same-session Codex generated images as rejected unless individually re-approved
- do not delete or disable the current `tool-nook-entry.png` merely because of its filename; inspect the installed asset and references first
- convert only user-provided, approved source PNGs into game-ready assets
- do not generate new art inside Codex for this pass
- do not wire converted assets into `src\assets\` until the user explicitly approves the source image and installation step
- live-review the installed selector board, worker-break door, compost/sign layout, plot outline, companion speed, and image-backed Herbalist Workbench before broad new art installation

## Sources

- [[short-term/2026-05-13-glassroot-garden-worker-final-decommission-report]]
- [[short-term/2026-05-13-glassroot-garden-asset-conversion-restart-report]]
- [[short-term/2026-05-16-garden-worker-final-decommission-report]]
- [[short-term/2026-05-16-glassroot-garden-visual-artifact-pet-selector-report]]
- [[short-term/2026-05-16-glassroot-garden-starter-pets-selector-wiring-report]]
- [[short-term/2026-05-16-glassroot-garden-worker-break-portal-door-layered-animation-report]]
- [[short-term/2026-05-18-glassroot-garden-worker-report]]
- [[short-term/2026-05-19-glassroot-garden-worker-final-decommission-report]]
