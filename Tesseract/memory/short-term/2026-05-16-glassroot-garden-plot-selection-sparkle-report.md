# Glassroot Garden Plot Selection Sparkle Report

Date: 2026-05-16
Worker: Bob / Codex
Scope: Glassroot Garden / The Garden World Key
Project path: `C:\Users\yrred\Desktop\Unity\TWB-Farming`

## What Changed

- Added a runtime-generated plot selection sparkle texture.
- Added a particle emitter field for each garden plot.
- Empty selectable plots now show a color-shifting magical sparkle field on hover instead of the old outline highlight.
- Clicking an empty selectable plot keeps the sparkle field running while the seed bag is open and no seed packet has been selected.
- Selecting a seed packet stops the persistent sparkle field.
- Existing selected/hover outline behavior remains available for non-empty plot/info interactions.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-plot-selection-sparkle-report.md`

## Tests / Checks Run

- `npm run build`: passed.
- Browser interaction smoke at `http://127.0.0.1:5173/`: passed.
  - Opened the garden.
  - Hovered an empty plot.
  - Clicked the plot to open the seed bag.
  - Clicked a seed packet.
  - No console errors or page errors were reported.
- Visual smoke screenshots were temporarily captured and inspected during the pass.

## Cleanup Performed

- Removed temporary Playwright smoke screenshots from `output\playwright`.

## Risks

- The effect uses one stopped/started particle emitter per plot. Twelve emitters is reasonable for this scene, but if the garden scales up later, a pooled/shared emitter approach may be cleaner.
- The seed bag still uses the existing two-step flow: choose seed packet, then press `Plant Selected`. The sparkle field stops at seed-packet selection per the user request, not at final planting queue.

## Memory-Worthy Notes

- Plot selection UX direction changed from static outline emphasis to a magical particle field over the bed.
- The persistent particle state represents "this bed is waiting for seed selection," and intentionally clears once a seed packet is chosen.

## Follow-Up Recommendations

- If the user likes the direction, tune sparkle density/color once viewed live in Chrome at the user's normal zoom.
- Later, consider different sparkle palettes for soil state, crop tier, or magical crop families.

## Anything Blocked

- Nothing blocked.
