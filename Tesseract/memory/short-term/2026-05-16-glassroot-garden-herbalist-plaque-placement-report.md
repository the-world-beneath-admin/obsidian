# Glassroot Garden Herbalist Plaque Placement Report

## Task
Move the herbalist hut marker plaque to the right side of the herbalist door, centered in the wall space between the door edge and the garden wall edge, and place it one render layer behind the animated door.

## Result
The herbalist plaque now uses a measured right-side wall-bay position. Its center is calculated from the animated door's visual right edge and the garden wall's right edge, producing an x-position of about 1198. The door marker plaques render at depth 1, and the herbalist animated door renders at depth 2, so any overlapping open-door art will cover the plaque instead of the plaque floating on top.

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced during this pass. A clean screenshot and a debug ready-crop harvest/deposit screenshot were captured without the earlier all-plots plant/bar artifact.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-herbalist-plaque-placement-report.md`

## Assets Converted Or Explicitly Not Converted
No assets were converted or generated. This was a scene placement and render-depth change only.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-plaque-right-side-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-plaque-door-open-depth-2026-05-16.png`

## Checks Run
- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming`; passed.
- Playwright screenshot at `1280 x 720` for the static plaque placement.
- Playwright debug harvest/deposit screenshot to verify the plaque/door depth while the herbalist door is open.

## Cleanup Performed
No temporary scratch files were created for this change. The two Playwright screenshots were kept as evidence.

## Risks
The current open-door art does not visibly overlap much of the right-side plaque, so the depth fix is correct but only lightly demonstrated by the present frames. If future door art swings farther right, the plaque will already be behind the door.

## Memory-Worthy Notes
The right-side herbalist plaque position is derived from the animated door's display edge and `GARDEN_ARCHITECTURE_RIGHT`, rather than being hand-placed on the old left-side wall bay. Door marker plaque depth is now one layer behind the herbalist animated door.

## Do Not Promote To Memory
Do not promote the temporary visual tuning details unless this plaque placement becomes the approved final Garden wall standard.

## Next Recommended Gate
Have the user approve the right-side plaque placement in the live browser, then continue with the middle tool shed door sheet only after the static wall plaques still read clearly.
