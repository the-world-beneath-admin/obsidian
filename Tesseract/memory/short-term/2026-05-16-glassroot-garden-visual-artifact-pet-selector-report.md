# Glassroot Garden Visual Artifact / Pet Selector Report - 2026-05-16

## Task

Scope: The World Beneath parent project, The Garden World Key, source/internal name Glassroot Garden.

Investigate the user-visible issue where all 12 plots showed mature-looking plant artifacts and blue bars in the live browser after the interrupted pet-selector rollback. Do not install the pet selector board until the artifact is reproduced, explained, fixed, or explicitly deferred.

## Result

Fixed a latent startup-order visual bug in `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.

The plot plant shapes, optional-work bars, and state badges were being created visible by default in `createPlotGrid()` and hidden later by `refreshAllPlots()`. If any runtime error occurred after plot creation but before `refreshAllPlots()`, every plot displayed default plant geometry and the default blue optional-work bar. This matches the user-reported symptom and explains why clean Playwright after rollback did not reproduce it: with no startup error, the refresh hid the placeholder plant/bar objects.

The fix creates those plot child objects hidden by default. `refreshPlot()` remains responsible for showing them only when a plot state actually needs them.

The pet selector board was not installed.

## Whether The Plant/Bar Artifact Was Reproduced

- Clean Playwright with no local save: did not reproduce the artifact.
- Read-only browser-state search: no currently running Chrome/Edge debug session was available. A read-only LevelDB scan found old Codex in-app browser saves from 2026-05-12 with 9 plots and 0 planted crops, but no current parseable 12-plot/crop save matching the user report.
- Seeded all-growing save test: produced all-plots plant visuals and work bars as an expected saved-game state, but not the exact default blue-bar failure mode.
- In-memory Playwright fault injection reproduced the reported failure shape by simulating the old default-visible plot children plus a startup error before `refreshAllPlots()`.
- In-memory Playwright fault injection after the fix confirmed the same simulated startup error no longer leaves plant/bar artifacts on empty plots.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-visual-artifact-pet-selector-report.md`

## Assets Converted Or Explicitly Not Converted

No assets were converted.

No pet selector asset was installed. `src\assets\glassroot\garden\pet-selector-board.png` remains absent, and no live `pet-selector-board` scene references were found.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-visual-artifact-clean-2026-05-16-wait10.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-visual-artifact-seeded-all-growing-before-fix.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-visual-artifact-clean-after-fix-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-visual-artifact-fault-injection-old-defaults-repro-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-visual-artifact-fault-injection-after-fix-2026-05-16.png`

One earlier 3-second screenshot was black due to capture timing and was kept as evidence:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-visual-artifact-clean-2026-05-16.png`

## Checks Run

- `npm run build` before changes: passed.
- Started local Vite dev server at `http://127.0.0.1:5173/` for browser checks.
- Captured clean 1280 x 720 Playwright screenshot after the fix.
- Ran read-only local browser storage search for `twb.glassrootGarden.save.v1`.
- Ran seeded-save Playwright check with all 12 plots growing.
- Ran in-memory fault-injection Playwright checks before/after the visibility-default fix.
- `npm run build` after changes: passed. The expected Vite large Phaser chunk warning remains.

## Cleanup Performed

- Stopped the local Vite dev server after verification.
- No source temp files were created.
- Fault-injection changes were in-memory Playwright route transforms only; no temporary source patches were written.
- Screenshot evidence and `output\playwright\dev-server-visual-artifact.log` were kept under the allowed evidence folder.

## Risks

- A normal saved game with all 12 plots planted will still show plant geometry and plot work/status bars; that is expected gameplay, not the startup artifact.
- Future startup errors can still stop later render passes, but the specific empty-plot plant/bar artifact is guarded against.
- `GlassrootGardenScene.ts` remains monolithic, so render-order failures are still easy to create during visual integration.
- The user's exact live browser state could not be inspected through a live Chrome/Edge debug port; only read-only storage artifacts were available.

## Memory-Worthy Notes

- The artifact was caused by render object default visibility, not new art.
- Plot child objects should be born hidden and shown only through `refreshPlot()`.
- Clean Playwright alone was not sufficient as a diagnostic, but fault injection plus local-storage inspection explained the clean/user divergence.
- The pet selector board remains blocked on explicit install approval and edge/cyan cleanup review.

## Do Not Promote To Memory

- Do not promote the fault-injection script details as permanent process.
- Do not promote the seeded all-growing save as a real user save.
- Do not promote the black 3-second screenshot except as a capture-timing warning.

## Next Recommended Gate

Bob/orchestrator should review this report, then decide whether to ask the user for explicit approval to install the preserved pet selector board candidate. If approved, recheck the candidate edge/cyan cleanup first, install from `pet-selector-plaque-01`, keep companion hit areas/home points intact, run `npm run build`, and capture a fresh 1280 x 720 screenshot.
