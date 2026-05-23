# Glassroot Garden Plant Placement Tuning Report

## Task

Improve the visible placement of newly wired plant sprites after the user confirmed they appeared, but not in a good position on the plots.

## Result

Adjusted plot plant layout so crop sprites use a consistent soil-centre anchor instead of the older bottom anchor. The top optional-action badge was moved above the bed, and the lower plot state badge was reduced and shifted onto the bed frame so it no longer sits over the plant art.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`

## Assets Converted Or Explicitly Not Converted

No assets were converted. This was a scene layout and sizing pass only.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-plant-placement-tuned-1280x720.png`

## Checks Run

- `npm run build` passed.
- Playwright captured a 1280 x 720 staged browser screenshot at `http://127.0.0.1:5173/`.

## Cleanup Performed

No temporary source files were created. The screenshot was kept under the approved `output\playwright\` folder as visual evidence.

## Risks

The state badge is now intentionally tucked onto the lower-left frame area; if the preferred direction is zero overlap with the plot frame, that badge should be moved to a separate UI layer outside the bed entirely.

## Memory-Worthy Notes

The plant sprites themselves were centred in their PNG canvases. The visible placement problem came from scene anchoring and badge overlap, not bad crop asset centering.

## Do Not Promote To Memory

Do not promote exact screenshot names or staged save data.

## Next Recommended Gate

Refresh the live Garden browser and confirm whether the plot crop art now reads as planted in the soil bed rather than being crowded by UI badges.
