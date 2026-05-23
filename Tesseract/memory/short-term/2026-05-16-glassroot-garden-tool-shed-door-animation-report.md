# Glassroot Garden Tool Shed Door Animation Report

## Task
Cut out the user-provided cyan-background middle tool shed sprite sheet, clean cyan and near-cyan edge tones properly, install the cleaned sheet, and wire it into the Garden scene as an animated tool shed door.

## Result
The tool shed sprite sheet is installed and animated. Pets now open the middle tool shed door when fetching a hoe, seeds, wards, or shears, then the door closes after they leave. The cleaned sheet uses 6 frames at 362 x 412 each, cropped from the uploaded 2172 x 724 source into a 2172 x 412 installed sheet.

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced during this pass. The test used a clean local save and a normal planting path; no all-plots mature plant or blue-bar artifact appeared.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\tool-shed-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\tool-shed-open-close-01\source\tool-shed-open-close-source.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\tool-shed-open-close-01\crops\tool-shed-open-close-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\tool-shed-open-close-01\qa\tool-shed-open-close-qa-dark.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\tool-shed-open-close-01\qa\tool-shed-open-close-qa-light.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-tool-shed-door-animation-report.md`

## Assets Converted Or Explicitly Not Converted
Converted the uploaded source `C:\Users\yrred\Downloads\ChatGPT Image May 16, 2026, 12_24_37 AM.png` into `tool-shed-open-close-sheet.png`. The cleanup used a multi-stage matte pass: near-exact cyan removal, edge-connected cyan-family removal, then transparent-contour removal of darker cyan/teal edge tones. No new art was generated in Codex. No other door sheets were converted.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-tool-shed-door-static-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-tool-shed-door-arrival-4200ms-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-tool-shed-door-arrival-5200ms-2026-05-16.png`

## Checks Run
- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming`; passed.
- Dark and light QA sheets inspected after edge cleanup.
- Playwright `1280 x 720` static screenshot captured.
- Playwright planting path exercised from a clean local save; verified the tool shed door opens while the pet reaches the tool shed and closes after departure.

## Cleanup Performed
Removed experimental edge-tone test crops, enlarged edge-debug zooms, and timing screenshots that missed the useful open/closed states. Kept the source copy, final cleaned crop, final dark/light QA sheets, and three useful Playwright evidence screenshots.

## Risks
The new tool shed sheet is about 1.42 MB and contributes to the existing Vite large-chunk warning. The in-game display uses the existing tool shed footprint of 190 x 120, so the asset is intentionally compressed into the current wall layout. Multiple simultaneous pet visits could restart the same door animation, which is acceptable for now but may need a small door-state queue later.

## Memory-Worthy Notes
The user explicitly corrected the cleanup process: cyan cutouts must remove not only exact cyan but also near-cyan and darker cyan-adjacent tones around the border. The final tool shed pass used exact/near-exact matte removal, edge-connected cyan-family cleanup, and a contour-only edge-tone removal pass. Tool shed actions currently include hoe fetch, seed fetch, ward fetch, and shears fetch.

## Do Not Promote To Memory
Do not promote the intermediate missed timing screenshots or experimental edge-tone test files. They were temporary QA artifacts and have been removed.

## Next Recommended Gate
User visual approval in the live browser, then proceed to the final portal/pet door two-layer sheet when the source assets are ready.
