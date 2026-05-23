# Glassroot Garden Herbalist Door Alignment And Timing Report

## Task
Investigate the user video showing the new herbalist hut door animation sitting slightly left, a small black artifact near the upper-left of the animation, and timing that did not line up with pets depositing harvested goods. Apply the requested additional 5-pixel right adjustment.

## Result
The herbalist door animation was corrected and retimed. The animated door now uses a +10 px center offset from the first placement pass, including the latest requested 5 px move to the right. The black orphan artifacts were removed from the sheet frames. Door behavior is now split into open and close animation phases: it opens when the pet reaches the herbalist door to deposit goods, stays open during the deposit hold, and closes after the pet starts leaving.

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced during this follow-up. The Playwright check used a deliberate ready-crop debug seed to exercise the pet harvest/deposit path; no all-plots mature plant or blue-bar artifact appeared during this door pass.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\herbalist-door-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-door-open-close-01\qa\herbalist-door-open-close-qa-dark.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-door-open-close-01\qa\herbalist-door-open-close-qa-light.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-herbalist-door-alignment-timing-report.md`

## Assets Converted Or Explicitly Not Converted
No new image-generation pass was performed. The existing user-provided cyan-background herbalist door sheet was cleaned in place with a component-based border artifact pass. Four small orphan components were removed from frames 1-4 near the left edge/top-left region. No tool shed or pet door animation sheets were created or converted in this pass.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-door-retimed-9500ms-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-door-retimed-10500ms-2026-05-16.png`

## Checks Run
- Inspected the supplied screen recording from `C:\Users\yrred\AppData\Local\Packages\Microsoft.ScreenSketch_8wekyb3d8bbwe\TempState\Recordings\20260516-0454-01.2467792.mp4`.
- Rebuilt the browser project with `npm run build`; build passed.
- Exercised the pet harvest/deposit path in Playwright at `http://127.0.0.1:5173/` using the existing debug ready-crop hook.
- Verified the door is open while the pet is at the herbalist hut deposit point and closed after the pet leaves.

## Cleanup Performed
Temporary video montage and extra timing screenshots from intermediate checks were removed. The two useful timing screenshots listed above were kept as evidence.

## Risks
The pet still renders in front of the doorway rather than being occluded by the room/door depth. This may be acceptable for now, but if the desired read is that the pet truly enters the room, a small occlusion/fade/depth handoff should be added next. The animated herbalist door sheet is large and contributes to the existing Vite large chunk warning. Only the herbalist door animation was corrected here; tool shed and pet door animations remain future work.

## Memory-Worthy Notes
The herbalist door sheet needs a +10 px render-center correction to visually match the original right-hand door placement. The deposit flow reads better when the door opens on arrival, remains open through the deposit hold, and closes after the pet leaves rather than playing as one short timed burst. Component cleanup on cyan-cut sheets should include a small-orphan pass after the cyan and near-cyan removal pass.

## Do Not Promote To Memory
Do not promote the intermediate timing screenshots, the temporary video montage, or the exact debug seed sequence. These were implementation evidence only.

## Next Recommended Gate
Have the user visually approve the retimed herbalist door in the live browser. If approved, the next gate should decide whether to add pet occlusion/fade at the doorway before producing matching tool shed and pet door animation sheets.
