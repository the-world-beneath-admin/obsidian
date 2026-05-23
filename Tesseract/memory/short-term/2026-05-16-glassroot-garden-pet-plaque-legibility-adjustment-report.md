# Glassroot Garden Pet Plaque Legibility Adjustment Report - 2026-05-16

## Task
Adjust the newly wired starter pet selector plaque before further expansion: remove the circular rings, make the pet sprites readable on a pale backing inside each frame, enlarge the plaque by 15%, and move it up 15 pixels.

## Result
Completed.

- Removed the circular selector rings from the pet plaque slots.
- Added pale framed rectangular backing panels behind Chuck, Peggy, and Stanly.
- Increased the pet selector board display from `210 x 86` to `242 x 99`.
- Moved the board center from `y = 111` to `y = 96`.
- Adjusted slot spacing from `[-62, 0, 62]` to `[-71, 0, 71]` to match the larger plaque.
- Kept the board in the pink-square wall area.
- Tool shed and herbalist hut plaques remain visible in the verification screenshot.

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced in this clean Playwright pass.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-pet-plaque-legibility-adjustment-report.md`

## Assets Converted Or Explicitly Not Converted
No assets were converted. No new art was generated.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-plaque-legibility-2026-05-16.png`

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
- The pale backing panels improve readability but may need one more art-direction pass if the final target is diegetic parchment, glass, or enamel rather than plain light backing.
- The plaque is now closer to the upper wall trim after the requested upward shift.

## Memory-Worthy Notes
- Garden starter pet plaque uses no circular slot rings after this adjustment.
- Board size is now 15% larger and positioned 15 pixels higher than the prior starter-pet wiring pass.

## Do Not Promote To Memory
Do not promote directly. Bob/orchestrator should review and decide whether this visual adjustment is accepted as durable.

## Next Recommended Gate
Review the screenshot in-browser and approve the plaque size, vertical position, and pet readability before adding more selector behavior.
