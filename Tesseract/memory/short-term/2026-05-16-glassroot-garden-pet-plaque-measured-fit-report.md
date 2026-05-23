# Glassroot Garden Pet Plaque Measured Fit Report - 2026-05-16

## Task
Measure the actual usable pet-frame space in the selector plaque, sample 15 random pet icons from the 300+ Unity pet icon set, use visible alpha bounds to size the starter pets so they fill the frame, and center each pet's visible body on the usable frame center.

## Result
Completed.

- Measured the transparent cutout components in `pet-selector-board.png`.
- Replaced rough slot offsets with measured usable-frame centers.
- Enlarged the khaki backing panels to fill the measured usable cutouts.
- Removed the prior arbitrary down-left offset and set each pet origin to the visible alpha-bounds center.
- Set per-pet selector display sizes:
  - Chuck: `56`
  - Peggy: `59`
  - Stanly: `60`
- Kept the board art above the backing/sprites so the board visibly frames them.

## Measurement Notes
Board source image:

- Natural size: `1028 x 419`
- Display size in scene: `242 x 99`

Measured usable frame windows at scene scale:

- Left: center offset `-66.03, 11.11`, usable `40.02 x 46.78`
- Middle: center offset `-1.06, 11.22`, usable `40.49 x 47.02`
- Right: center offset `63.32, 10.99`, usable `39.78 x 46.55`

Sampled 15 non-special pet icons from `Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons` with a deterministic seed. Average visible alpha bounds:

- Average visible width ratio: `0.8173`
- Average visible height ratio: `0.7499`
- Average visible bounds: `836.9 x 767.9`
- Baseline square display size from the sample average: about `49 px`

The starter pet PNGs had more transparent padding than the sampled average, especially Chuck, so the final pass used the sample average as a sanity baseline but used exact starter-pet alpha bounds for per-pet fit and origin centering.

Starter-pet visible alpha origin centers:

- Chuck: `0.523, 0.500`
- Peggy: `0.483, 0.473`
- Stanly: `0.500, 0.482`

## Whether The Plant/Bar Artifact Was Reproduced
Not reproduced in this clean Playwright pass.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-pet-plaque-measured-fit-report.md`

## Assets Converted Or Explicitly Not Converted
No assets were converted. No new art was generated.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-plaque-measured-fit-2026-05-16.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-starter-pet-plaque-measured-fit-crop-2026-05-16.png`

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
- Chuck is naturally much narrower than the usable frame because his accepted source art is vertically dominant; he now fills the frame height but will not fill the full width without distortion or cropping.
- The sample-average method alone would under-size the starter trio, so the implemented values use exact starter alpha bounds after the sample-baseline calculation.

## Memory-Worthy Notes
- Selector pet placement now uses measured board cutouts rather than rough offsets.
- Starter pet selector icons now use alpha-bounds origins so visible pet bodies, not transparent canvases, are centered in their frames.

## Do Not Promote To Memory
Do not promote directly. Bob/orchestrator should review the screenshot and decide whether the measured fit is accepted as durable.

## Next Recommended Gate
Review the crop screenshot for final pet-frame readability. If accepted, keep these measured constants as the selector baseline before adding more behavior.
