# 2026-05-16 Glassroot Garden Pet Speed, Tags, and Action Label Report

## Task
Slow starter pet movement by half again, remove persistent tags/name/focus labels around roaming pets, and show overhead text only for actual plot-work actions rather than roaming/walking states.

## Result
Implemented in `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.

- Pet travel timing was slowed again by increasing companion movement duration and min/max travel duration.
- Persistent companion name/focus tags remain created for model compatibility but are no longer shown during roaming or movement.
- Roaming, returning, and source-fetch movements do not show overhead action text.
- Plot-work movements now show a small overhead action label on the pet, mounted inside the moving pet container so it follows the sprite reliably.
- Action labels linger briefly at the plot action point before the callback proceeds.
- Tool shed and herbalist hut plaques remained visible in the final 1280 x 720 screenshots.

## Whether the Plant/Bar Artifact Was Reproduced
Not reproduced in this pass. Clean Playwright screenshots did not show mature-looking plants or blue bars over all 12 plots. The action-label verification screenshot intentionally seeded one ready Basil crop through the existing debug hook, so that single plot shows the existing crop/harvest placeholder and plot status UI.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-pet-speed-tags-action-label-report.md`

## Assets Converted or Explicitly Not Converted
No new assets converted. Existing installed starter pet icon and walk-sheet assets were reused.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-pets-slower-no-roaming-tags-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-pets-action-label-visible-2400ms-2026-05-16.png`

## Checks Run
- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- Playwright 1280 x 720 clean roaming screenshot captured.
- Playwright 1280 x 720 debug-seeded harvest screenshot captured to verify the action label appears above the pet for plot work.

## Cleanup Performed
Removed 32 intermediate timing screenshots created while finding the correct action-label capture window. Kept only the two final evidence screenshots listed above.

## Risks
- The action label appears while the pet travels to the plot action point and briefly on arrival. This was chosen so the label is visible to the player; if the desired behaviour is strictly only during the stationary arrival beat, the label can be made arrival-only again but will need a longer dwell.
- Existing plot status labels such as `Harvesting` and `Lockdown` were not changed.
- Vite still reports the existing large chunk warning during build.

## Memory-Worthy Notes
- Companion source/walking labels should stay quiet unless the movement is actual plot work.
- For visual QA on this setup, rebuild before Playwright capture because the local `127.0.0.1:5173` page may behave like a built preview rather than hot-reloading source immediately.

## Do Not Promote To Memory
Do not promote this worker report directly to permanent memory. Bob/orchestrator should review and distill only the durable result and any accepted UI behaviour.

## Next Recommended Gate
User visual approval of slower roaming speed and plot-action-only pet labels, then continue to the next pet behaviour or Garden UI polish gate.
