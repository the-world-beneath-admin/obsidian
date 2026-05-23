# Glassroot Garden Pet Plaque Framed Khaki Adjustment Report - 2026-05-16

## Task
Remove pet names from the selector plaque, place the pet sprites on tan/khaki backing, render the pet panels behind the plaque art so the plaque frames them, and move the slot contents down-left by 5 pixels.

## Result
Completed.

- Removed visible pet name/focus text from the selector plaque.
- Changed pet backing panels from pale white/parchment to khaki/tan.
- Set selector backing/sprite depth below the plaque image and the board depth above them so the plaque frames the pet sprites.
- Added `PET_SELECTOR_SLOT_CONTENT_X_OFFSET = -5` and `PET_SELECTOR_SLOT_CONTENT_Y_OFFSET = 5`.
- Kept board size and wall placement from the previous pass.

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced in this clean Playwright pass.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-pet-plaque-framed-khaki-adjustment-report.md`

## Assets Converted Or Explicitly Not Converted
No assets were converted. No new art was generated.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-plaque-framed-khaki-2026-05-16.png`

## Checks Run
- `npm run build`
  - Passed.
  - Vite large-chunk warning remains.
- Playwright 1280 x 720 visual capture against `http://127.0.0.1:5173/`
  - Passed.
  - Browser console only showed repeated WebGL `ReadPixels` performance warnings during screenshot capture.

## Cleanup Performed
No temporary scratch files were created. The normal Vite `dist` folder was refreshed by the build.

## Risks
- The khaki panels are now framed by the board image, but their exact shade may need art-direction tuning after live review.
- Selector selected-state indication is now subtle because the slot content is intentionally behind the plaque frame.

## Memory-Worthy Notes
- Garden pet selector slots no longer show pet names or focus labels.
- Pet slot backing/sprites render behind the selector plaque image as a framed inset.

## Do Not Promote To Memory
Do not promote directly. Bob/orchestrator should review and decide whether this visual adjustment is accepted as durable.

## Next Recommended Gate
Review the live browser screenshot for khaki shade and sprite centering before adding more pet-selector behavior.
