# Glassroot Garden Selected Plot Sparkle Report

## Scope

- World Key: The Garden / Glassroot Garden.
- Project: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Owned source file: `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.

## What Changed

- Replaced the previous dormant per-plot sparkle emitter wiring with one scene-level Phaser particle emitter for the currently selected plot.
- Kept the generated runtime particle texture path; no external art was added.
- Constrained sparkle emission to a soft oval inside the usable bed area so it follows the plot shape instead of filling a large square overlay.
- Tuned the selected-plot sparkle to small cream, gold, and soft green motes with short lifespan and low emission rate.
- Added scene shutdown cleanup for the selected-plot emitter.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-selected-plot-sparkle-report.md`

## Tests / Checks Run

- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- Captured a 1280x720 Playwright screenshot after selecting plot 1:
  - `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\selected-plot-sparkle-1280x720.png`

## Cleanup Performed

- No broad cleanup was performed.
- No temporary source, scratch, or log files were created by this task.
- Screenshot evidence was intentionally retained under `output\playwright`.

## Risks

- The sparkle is intentionally subtle; live review should confirm it is visible enough during motion without competing with plants, plot labels, or seed-bag UI.
- Screenshot evidence captures a moment in the particle cycle, so live browser review is still the better final gate for feel and readability.

## Memory-Worthy Notes

- Selected plot sparkles now use one movable Phaser emitter instead of twelve per-plot emitters.
- The existing generated plot sparkle texture remains the source for the effect.

## Follow-Up Recommendations

- Live review at `http://127.0.0.1:5173/` should confirm the sparkle reads clearly when switching plots and that it stops cleanly when selection is cleared.
