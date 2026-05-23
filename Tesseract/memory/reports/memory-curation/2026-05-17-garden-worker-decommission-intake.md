# Garden Worker Decommission Intake

## Status

Complete - 2026-05-17.

## Source Reviewed

- [[short-term/2026-05-17-garden-worker-final-decommission-report]]

## Scope

World Key: The Garden.

Internal/source name: Glassroot Garden / TWB-Farming.

Project path:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming
```

## Promoted

- Active scene remains `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.
- `npm run build` passed on 2026-05-17 after the Notice Board duplicate-order guard.
- Local dev server returned HTTP `200` at `http://127.0.0.1:5173/`.
- The starter-pet selector board is installed and replaces the old circular selector as current visual direction.
- Chuck, Peggy, and Stanly are wired with plaque icons and moving sprite sheets.
- Door animation passes exist for herbalist/storage hut, tool shed, and worker-break/pet-shed portal/door layers.
- Pet tokens are intentionally kept above door layers.
- The Garden now has tiered plot, well, compost, and compost-fill visuals wired.
- The seed bag is image-backed with tier tabs and larger seed cards.
- Plant sprites are wired for current crop stages across the crop list.
- Plot timers were moved into the plot info panel.
- Drying-room occupied slots can be inspected, and ready bundles can be manually collected while the room is open.
- Raw/dried herbalist storage uses mobile-friendlier summary cards rather than tiny slot grids.
- Notice Board quest bundles are one-off orders: open -> awaiting completion -> complete.
- Duplicate Notice Board quest-bundle production is blocked once queued or completed.
- Transfer Bundles remain repeatable.
- The all-plots plant/bar artifact was not reproduced in clean Playwright and should remain treated as a live browser/save-state risk if it appears again.

## Kept Report-Only

- Exact pet speed, door delay, plaque offset, and sprite placement tuning values.
- Screenshot list and dev-server log minutiae.
- Prompt drafts and interim generated-sheet attempts.
- Current bundler/packing machine drawing as final art direction.

## Warnings

- `GlassrootGardenScene.ts` is very large and now carries many systems, so future edits are regression-prone.
- Door, portal, plaque, and pet depth ordering is sensitive and should be screenshot-verified after visual changes.
- Existing local saves may hold older queued bundles, selected recipes, or plot states that behave differently than clean Playwright.
- No formal unit/integration test suite exists; build and browser automation remain the primary checks.
- The Vite large chunk warning remains.

## Files Changed

- `memory/briefs/current-glassroot-garden-task.md`
- `memory/briefs/current-game-dev-task.md`
- `memory/wiki/world-keys/the-garden/overview.md`
- `memory/wiki/world-keys/the-garden/systems.md`
- `memory/wiki/world-keys/the-garden/testing.md`
- `memory/wiki/world-keys/the-garden/decisions.md`
- `memory/wiki/world-keys/the-garden/open-questions.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\glassroot-garden-worker\HYDRATION_PROMPT.md`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\glassroot-garden-worker.toml`

## Remains Blocked

- Notice Board / finished bundle lifecycle validation on active saves.
- Future daily/rotating Notice Board order design.
- Replacement of the prototype bundler/packing machine with a layered art approach.
- Mobile/touch validation of storage cards and seed bag.
- Save migration/compatibility coverage.

## Next Gate

Hydrate a fresh visible `glassroot-garden-worker` window with:

```text
C:\Users\yrred\Documents\New project 2\glassroot-garden-worker\HYDRATION_PROMPT.md
```

The next worker should harden the Notice Board / finished bundle lifecycle first. Do not start the packing-machine art pass unless the user explicitly redirects.
