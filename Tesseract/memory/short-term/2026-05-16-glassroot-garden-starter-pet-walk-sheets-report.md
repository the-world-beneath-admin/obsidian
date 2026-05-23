# Glassroot Garden Starter Pet Walk Sheets Report - 2026-05-16

## Task
Wire the actual Chuck, Peggy, and Stanly walk sprite sheets into the moving Garden pets.

## Result
Completed.

- Copied the finished 4-direction starter pet walk sheets into Garden assets.
- Loaded them with Phaser `load.spritesheet`.
- Registered per-pet walk animations for rows `down`, `left`, `right`, and `up`.
- Replaced the moving pet token's static icon with a Phaser `Sprite` using the walk sheet.
- Movement now chooses the animation row from each path segment:
  - left/right for horizontal travel
  - up/down for vertical travel
- Pets return to frame `00` of their current facing direction when idle.
- The selector plaque icons remain the static measured-fit versions from the previous pass.

## Sprite Sheet Contract Used
- Canvas: `1024 x 1024`
- Grid: `4 x 4`
- Cell: `256 x 256`
- Row order: `down`, `left`, `right`, `up`
- Column order: frames `00`, `01`, `02`, `03`
- Walk frame rate: `8 fps`

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced in this clean Playwright pass.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-chuck-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-peggy-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\starter-pet-stanly-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-starter-pet-walk-sheets-report.md`

## Assets Converted Or Explicitly Not Converted
No new art was generated and no sprite sheets were converted. Existing finished walk sheets were copied from:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-chuck-creature-special-ephemrial-spirit-chuck-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\util-peggy-creature-special-ephemrial-spirit-peggy-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-stanly-creature-special-ephemrial-spirit-stanly-walk-4dof-1024.png`

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-walk-sheets-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-walk-sheets-crop-2026-05-16.png`

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
- The moving pet sprite scale is currently set to `56` display pixels per 256px frame. This reads cleanly but may need a later art-direction nudge if the pets feel too small or too large in motion.
- Screenshot evidence is static; full animation smoothness should be judged in the live browser.
- The three added walk sheets increase the Garden asset payload by roughly 2.9 MB before compression.

## Memory-Worthy Notes
- Garden roaming starter pets now use real 4x4 walk sheets rather than static pet icon images.
- Directional rows follow the main Unity sprite-sheet contract: down, left, right, up.

## Do Not Promote To Memory
Do not promote directly. Bob/orchestrator should review and decide whether this runtime animation wiring is accepted.

## Next Recommended Gate
Review the live browser movement for scale, row direction, and animation speed before adding selection behavior or account-driven pet roster logic.
