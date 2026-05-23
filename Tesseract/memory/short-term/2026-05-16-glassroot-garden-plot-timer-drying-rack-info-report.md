# Glassroot Garden Plot Timer / Drying Rack Info Report

## Task
Move growing-plant timers off the main garden beds and into the plot info panel, make drying-rack plants clickable for drying-time inspection, and harden plot clicks so the info panel opens unless the plant is actively clickable for a care step.

## Result
Completed.

- Planted plots no longer render the countdown / ready text above the plant on the main garden screen.
- Growing plot info panels retain the live `Remaining` line, so the timer is available after clicking the plot.
- Plot clicks now fall through to the info panel for compost-only crops and already-queued care states instead of swallowing the click with a status message.
- Active optional care windows still take precedence and queue/attempt the care action.
- Drying rack occupied slots can now be clicked while still drying to show the remaining drying time.
- Ready drying-rack slots still collect into dried plant bins when clicked.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-plot-timer-drying-rack-info-report.md`

## Assets Converted Or Created
None.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-growing-plot-info-no-top-timers-1280x720.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-drying-rack-inspect-click-1280x720.png`

## Checks Run
- `npm run build` passed.
- Clean Playwright context at `http://127.0.0.1:5173/`.
- Seeded a synthetic growing Basil plot through localStorage and confirmed clicking it opened the plot info panel with `Remaining` inside the panel.
- Seeded a synthetic drying Basil rack slot and confirmed clicking it produced: `Basil is drying. Ready in 1m 57s.`

## Cleanup Performed
No temporary scripts were written. Playwright screenshots were intentionally kept as evidence.

## Risks
- The main garden now relies on the state badge/window badge plus the info panel for planted plot timing/status, so any future request for always-visible crop status should be handled as a deliberate HUD design pass.
- Drying rack still shows its small in-room timer text; this task only removed timers from main-screen planted plots.

## Memory-Worthy Notes
- For Glassroot Garden, planted plot countdowns now belong in the plot info panel rather than above the bed.
- Drying rack occupied slots should support click-to-inspect while drying and click-to-collect once ready.
- Plot info should open for non-actionable growing-plant clicks; active care-window clicks remain action-first.

## Do Not Promote To Memory
- The synthetic Playwright save data used for verification.
- Exact timing text from the test run.

## Next Recommended Gate
Have Bob/orchestrator review the interaction in the live browser, especially whether the remaining top-of-bed state badges are enough after removing the old countdown labels.
