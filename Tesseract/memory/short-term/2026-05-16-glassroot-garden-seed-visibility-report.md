# Glassroot Garden Seed Visibility Report

## Task

Respond to the user-visible issue that the yellow dot still looked like a placeholder seed and that the plant assets did not appear to have landed in the live Garden screen.

## Result

Fixed the seed presentation path. The crop plant PNGs were already wired and present in the build, but the seed-stage display was too small and the seed packet art still had a generic decorative dot. The live plot/action badge now uses the crop's real `seed-planted` sprite where available, with the old colored pip only as a fallback. Seed packet icons and plot seed-stage display were enlarged so the plant assets read more clearly.

## Whether The Plant Assets Landed

Yes. A clean Playwright runtime pass confirmed the plant asset folders are loaded and rendering in the browser. The build output also includes the `seed-planted`, `sprout`, `mature`, and `ready-harvest` PNG families.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_normal.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_hover.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_selected.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_locked.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\seed_packet_empty.png`
- Matching cleaned source copies under `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\crops-clean-alpha\`

## Assets Converted Or Not Converted

No new plant assets were converted. The existing 21 crop folders under `src\assets\glassroot\garden\plants\` each contain 8 PNG stages. The seed packet PNGs were lightly edited to remove their generic dot area so the runtime crop seed sprite is the visible marker.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-seed-bag-real-seeds-1280x720.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-seed-stage-real-sprites-1280x720.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-seed-marker-real-seeds-after-size-1280x720.png`

## Checks Run

- `npm run build` passed after the seed visibility edits.
- Playwright launched `http://127.0.0.1:5173/` in a clean browser context and captured 1280 x 720 screenshots.
- Runtime state check confirmed staged plots contained Basil, Thyme, Yarrow, and Sage crop ids.

## Cleanup Performed

No throwaway source files were created. Playwright screenshots were kept under the approved `output\playwright\` evidence folder.

## Risks

The user's open Chrome tab may still show older visual state until refreshed. The dev server is live, but browser cache or old local save timing can make the previous dot-like state linger visually.

## Memory-Worthy Notes

The herb plant sheets are present and render in-browser. The visible issue was seed-stage scale and marker presentation, not missing plant imports.

## Do Not Promote To Memory

Do not promote exact screenshot names or temporary visual-test save state. They are evidence for this pass only.

## Next Recommended Gate

Ask the user to hard-refresh the live Garden tab and confirm whether the seed-stage plots and optional action badge now read as real seed/plant sprites instead of placeholder yellow dots.
