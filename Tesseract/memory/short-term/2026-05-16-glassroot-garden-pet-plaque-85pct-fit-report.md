# Glassroot Garden Pet Plaque 85 Percent Fit Report - 2026-05-16

## Task
Back off the measured starter pet plaque images by about 15% because the prior fit was too large.

## Result
Completed.

- Reduced selector pet sprite display sizes to roughly 85% of the previous measured-fit values:
  - Chuck: `56` to `48`
  - Peggy: `59` to `50`
  - Stanly: `60` to `51`
- Preserved measured usable-frame centers, khaki backing dimensions, and alpha-bounds origins.
- Board framing, no-name layout, and khaki background remain unchanged.

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced in this clean Playwright pass.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-pet-plaque-85pct-fit-report.md`

## Assets Converted Or Explicitly Not Converted
No assets were converted. No new art was generated.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-plaque-85pct-fit-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-plaque-85pct-fit-crop-2026-05-16.png`

## Checks Run
- `npm run build`
  - Passed.
  - Vite large-chunk warning remains.
- Playwright 1280 x 720 visual capture against `http://127.0.0.1:5173/`
  - Passed.
  - Browser console only showed repeated WebGL `ReadPixels` performance warnings during screenshot capture.

## Cleanup Performed
No throwaway scratch files were left behind. The crop screenshot was intentionally preserved as review evidence.

## Risks
- The fit is now intentionally less edge-filling than the measured maximum. If the final art direction wants more aggressive fill, nudge up in smaller increments, likely 5% at a time.

## Memory-Worthy Notes
- Accepted measured frame centers/origins were preserved while reducing starter pet selector image scale to about 85%.

## Do Not Promote To Memory
Do not promote directly. Bob/orchestrator should review and decide whether this visual fit is accepted.

## Next Recommended Gate
Review the crop screenshot and approve the 85% fit or request a small directional nudge.
