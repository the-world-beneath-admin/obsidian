# Glassroot Garden Starter Pets Selector Wiring Report - 2026-05-16

## Task
Wire Chuck, Peggy, and Stanly into the Garden starter pet selector plaque, show their pet images in the plaque window and on the roaming companion tokens, and slow companion movement by 50%.

## Result
Chuck, Peggy, and Stanly now replace the placeholder companion trio in `GlassrootGardenScene.ts`.

- Chuck uses the Ward focus slot.
- Peggy uses the Tend focus slot.
- Stanly uses the Harvest focus slot.
- The selector plaque remains in the previously approved pink-square wall area.
- Each plaque slot now renders the corresponding starter-pet image.
- Roaming companion tokens now use the same starter-pet image sprites instead of plain circles.
- Companion movement duration was doubled by changing the per-pixel duration and clamps from the prior effective range to `4.4` ms/pixel with `280`-`1240` ms clamps.
- Tool shed and herbalist hut plaques remained visible in the verification screenshot.

## Whether The Plant/Bar Artifact Was Reproduced
Not part of this new change pass. The prior artifact fix remains in place; this pass did not reproduce mature plant or blue-bar artifacts in the clean Playwright capture.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-chuck.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-peggy.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-stanly.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-starter-pets-selector-wiring-report.md`

## Assets Converted Or Explicitly Not Converted
No new art was generated. No external image generation was used.

Copied existing role-specific starter pet PNGs from the main TWB Unity resource set into Garden assets:

- Chuck: `def-chuck-creature-special-ephemrial-spirit-chuck.png`
- Peggy: `util-peggy-creature-special-ephemrial-spirit-peggy.png`
- Stanly: `atk-stanly-creature-special-ephemrial-spirit-stanly.png`

The known invalid Peggy 1024 key-art was not used.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pets-wired-2026-05-16.png`

## Checks Run
- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming`
  - Passed.
  - Vite large-chunk warning remains.
- Playwright 1280 x 720 screenshot against `http://127.0.0.1:5173/`
  - Passed visual smoke check.
  - Console only reported repeated WebGL `ReadPixels` performance warnings during screenshot capture.

## Cleanup Performed
No temporary scratch files were created. The normal Vite `dist` output was refreshed by the build.

## Risks
- The copied starter images are 1254 x 1254 PNGs and are larger than needed for 30-40 px display. If load size becomes a concern, the next pass should create approved scaled derivatives from these same sources.
- The report memory still notes that Chuck art acceptance had previously been pending; this Garden pass uses the existing role-specific Unity asset because the user requested Chuck be wired into the Garden now.
- The selector labels are intentionally small to fit inside the board; final acceptance should be based on the live browser view.

## Memory-Worthy Notes
- Garden selector now uses the starter trio: Chuck / Peggy / Stanly.
- Garden companion movement speed was halved by doubling tween duration constants.
- Peggy uses the valid `util-peggy` asset rather than the removed invalid 1024 Peggy key-art.

## Do Not Promote To Memory
Do not promote this report directly. Bob/orchestrator should review the screenshot and decide what becomes permanent memory.

## Next Recommended Gate
Bob/orchestrator should review the screenshot, confirm the starter-pet icon alignment and roaming sprite scale/speed, then approve or request a narrow pixel/scale adjustment before broad Garden expansion.
