# The Garden Open Questions

## Current Questions

- Should Comfreygrass continue to create curing compost first, or should it eventually bypass curing and add ready compost directly?
- Should optional Feed Soil spend ready compost or stay a free Companion action?
- Should prototype persistence remain localStorage/local-save only for now, or should the next technical phase move toward Cloudflare/D1?
- What final art pipeline will replace Phaser placeholder shapes?
- How much tutorial scaffolding is needed for younger and older players to understand drying, compost, bundling, and transfer rules without debug-like UI?
- Should tier XP represent plant units, processed plants, contract completions, or a blended mastery model long-term?
- When should the large `GlassrootGardenScene.ts` file be split into systems, UI, data, and rendering boundaries?
- Does Notice Board XP intentionally stay formulaic (ingredient-count + mastery) or should it use recipe `boardXpReward` metadata (for example Greenward Order currently includes `boardXpReward: 12`)?
- Superseded - What exactly caused the user-visible mature plant sprites/artifacts and blue bars over all 12 plots? Current explanation is default-visible plot child objects when startup failed before `refreshAllPlots()`. Clean Playwright no longer reproduces it, but the user's active browser/save should still be watched.
- Should the lower plot state badge stay tucked onto the bed frame, or move to a separate UI layer once the live review settles?
- Superseded - Should the current pet selector board use the top source-sheet board candidate? The starter-pet board is now installed as the current selector direction.
- Should the pet selector board replace only the visual circular slots for now, or also open a real shared-inventory pet-swap modal later?
- Which current Garden environment assets are approved, merely acceptable for now, or explicitly do-not-use?
- How should one-off Notice Board orders reopen later if the game needs daily/rotating orders?
- Superseded - Should the next visual/art pass replace the prototype bundler/packing machine with a layered static-plus-small-animation asset? The 2026-05-19 v6 bundling-machine pass showed that a broad layered-machine prompt is too brittle unless the parts share anchors, sockets, and a single runtime footprint.
- What exact modular bundling-machine art contract should replace the failed v6 runtime path after reviewing SLYNYRD/external pixel-art composition references?
- Is the failed v6 bundling-machine runtime path currently visible in the app, and should it be hidden/reverted before the next prompt package is attempted?
- Superseded - Does the image-backed Herbalist Workbench remain usable on phone-sized/touch viewports, especially storage-bin scrolling, Notice Board selection, Bundler loading, and Back to Garden behavior? The 2026-05-19 focused review moved the direction to landscape-first phone handling because portrait Scale.FIT makes the room too small.
- Should Notice Board tiers with only three crop types eventually gain more crop variety, since tier 2 and tier 5 currently use the same three plants with varied order/quantities?
- What save migration/compatibility checks are needed after the recent seed bag, drying room, pet selector, and Notice Board lifecycle changes?
- What save migration/compatibility checks are needed after moving Notice Board and Transfer Bundle definitions into `src/data/bundleCatalog.ts`, especially for saves that persist posted order IDs?

## Sources

- [[short-term/2026-05-12-glassroot-garden-working-window-intake]]
- [[short-term/2026-05-16-garden-worker-final-decommission-report]]
- [[short-term/2026-05-17-garden-worker-final-decommission-report]]
- [[short-term/2026-05-18-glassroot-garden-worker-report]]
- [[short-term/2026-05-19-glassroot-garden-worker-final-decommission-report]]
