# 2026-05-16 Glassroot Garden Herbalist Door Animation Report

## Task
Cut out the provided cyan-background right-hand herbalist/storage door sprite sheet, install it into The Garden, and wire it so the door opens/closes when a pet stores a normal harvest at the door.

## Result
Implemented the right-hand herbalist/storage door animation in `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`.

- Converted the supplied 6-frame cyan sheet into a transparent Phaser spritesheet.
- Replaced the static right-hand storage/herbalist entry render with the animated door spritesheet.
- Added a Phaser animation for the 6-frame open/close cycle.
- Triggered the animation when a pet completes the `Store crop` delivery at the storage/herbalist door.
- Tool shed plaque, herbalist plaque, pet selector board, and pet sprites remained visible in the visual check.

## Whether the Plant/Bar Artifact Was Reproduced
Not reproduced during this pass. The Playwright verification used a debug-seeded Basil harvest to trigger the storage-door animation, so one plot intentionally showed harvest/lockdown UI. The all-plot mature plant/blue bar artifact was not seen.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\herbalist-door-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-door-open-close-01\herbalist-door-open-close-cyan-source.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-door-open-close-01\crops\herbalist-door-open-close-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-door-open-close-01\qa\herbalist-door-open-close-qa-dark.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\herbalist-door-open-close-01\qa\herbalist-door-open-close-qa-light.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-door-animation-9500ms-2026-05-16.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-herbalist-door-animation-report.md`

## Assets Converted or Explicitly Not Converted
Converted:

- Source: `C:\Users\yrred\Downloads\ChatGPT Image May 15, 2026, 11_19_50 PM.png`
- Installed: `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\herbalist-door-open-close-sheet.png`

Conversion notes:

- Source sheet was `2172 x 724`, 6 frames across.
- Each source frame was `362 x 724`.
- Shared cropped output frame size is `362 x 508`.
- First pass removed `740,524` border-connected cyan matte pixels.
- Second connected-edge cleanup removed `5,784` darker cyan/teal halo pixels.
- Final extra edge trim removed `6` remaining broad cyan-family edge pixels.

Not converted:

- Tool shed door sheet.
- Pet/break-room basement walkway door sheet.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herbalist-door-animation-9500ms-2026-05-16.png`

## Checks Run
- `npm run build` passed from `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Confirmed `http://127.0.0.1:5173/` responded with HTTP 200.
- Playwright 1280 x 720 capture verified the door opened during a debug-seeded storage delivery.

## Cleanup Performed
Removed six intermediate Playwright timing screenshots and kept only the best open-door verification screenshot.

## Risks
- Only the right-hand herbalist/storage door was supplied and installed. Tool shed and pet/break-room door animation still need their own cyan source sheets.
- The new door sheet is larger than the previous static store-entry asset and increases the built asset payload.
- The pet currently stands in front of the doorway while the door animates; if the desired effect is that the pet disappears behind the doorway, a separate depth/visibility timing pass is needed.
- Vite still reports the existing large chunk warning.

## Memory-Worthy Notes
- The cyan matte cleanup should remain a two-stage process: border-connected cyan removal first, then connected darker cyan/teal edge cleanup before install.
- The right-hand herbalist/storage door animation trigger is tied to normal harvest `Store crop` delivery.

## Do Not Promote To Memory
Do not promote this report directly to permanent memory. Bob/orchestrator should review and distill only the accepted asset pipeline and door-animation behaviour.

## Next Recommended Gate
User visual approval of the herbalist door opening/closing in browser, then create and install matching cyan-sheet animations for the tool shed door and pet/break-room basement door.
