# Glassroot Garden Worker Decommission Intake

## Status

Complete - 2026-05-16.

## Source Reviewed

- [[short-term/2026-05-16-garden-worker-final-decommission-report]]

## Scope

World Key: The Garden.

Internal/source name: Glassroot Garden.

Project path:

```text
C:\Users\yrred\Desktop\Unity\TWB-Farming
```

## Promoted

- The current Garden main scene remains `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.
- Latest worker reported `npm run build` passing after rollback of an interrupted pet selector board install.
- The current visible main screen uses approved PNG architecture/boundary assets, a `4 x 3` 12-plot layout, tier 1 plot art, grass ground tile, tier 1 well, tier 1 compost heap, and tool shed/herbalist door plaques.
- `SHOW_WALK_DEBUG_OVERLAY = false` is the latest reported state.
- The old circular pet selector remains live.
- The new pet selector board source/candidate is preserved under `output\asset-conversion\garden-main-screen\pet-selector-plaque-01\`, but it is not installed.
- The interrupted pet selector implementation was rolled back and should not be resumed as-is.
- The user-visible all-plots plant/bar artifact is unresolved. Clean Playwright after rollback did not reproduce the user's browser state, so local browser/save state may matter.
- The current asset conversion process should preserve source sheets and candidate crops under `output\asset-conversion\garden-main-screen\` before any install into `src\assets`.
- The cyan-background/black-outline cutout workflow remains the preferred Garden cutout standard.

## Corrected / Clarified

- Earlier isolated tool-nook art was rejected, but the filename `tool-nook-entry.png` is not automatically rejected. The current report says a wall-integrated `tool-nook-entry.png` is installed as part of the approved path, so future workers must inspect the current asset and references before changing or deleting it.

## Kept Report-Only

- Tiny coordinate nudge history.
- Exact intermediate screenshot sequence.
- Rejected old dirt-path attempt.
- The interrupted pet-board implementation details.
- Temporary guesses about plant artifacts.
- GPT prompt drafts and transient visual steering.

## Files Changed

- `memory/briefs/current-glassroot-garden-task.md`
- `memory/briefs/current-game-dev-task.md`
- `memory/wiki/world-keys/the-garden/overview.md`
- `memory/wiki/world-keys/the-garden/systems.md`
- `memory/wiki/world-keys/the-garden/testing.md`
- `memory/wiki/world-keys/the-garden/art-direction-and-asset-risks.md`
- `memory/wiki/world-keys/the-garden/open-questions.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\glassroot-garden-worker\HYDRATION_PROMPT.md`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\glassroot-garden-worker.toml`

## Remains Blocked

- Exact cause of the all-plots plant/bar artifact.
- Pet selector board installation.
- User decision on whether the top board crop is the final selector board.
- Any future shared-inventory pet-swap modal.

## Next Gate

Hydrate a fresh visible `glassroot-garden-worker` window with:

```text
C:\Users\yrred\Documents\New project 2\glassroot-garden-worker\HYDRATION_PROMPT.md
```

The worker should diagnose the visual artifact first, then only proceed to a narrow pet selector board pass if safe.
