# 2026-05-16 Glassroot Garden Seed Bag UI Wiring Report

## Task
Wire the cleaned seed bag UI asset set into the live Glassroot Garden seed bag panel.

## Result
The seed bag panel is now image-backed instead of rectangle-placeholder-backed.

The live panel uses the cleaned alpha crops for:

- main seed bag panel
- close button states
- seed packet normal, hover, selected, and empty states
- small navigation button states
- Plant Selected button states

Runtime crop names, page count, tier text, instructions, and button labels remain Phaser text over the UI art.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\*.png`

## Assets Converted Or Installed
Installed 40 cleaned seed bag UI PNG crops from:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\crops-clean-alpha\`

to:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\ui\seed-bag\`

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-seed-bag-ui-wired-1280x720.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-seed-bag-ui-debug-1280x720.png`

## Checks Run
- `npm run build` passed after wiring.
- Playwright visual check at 1280 x 720 passed.
- Playwright interaction check:
  - selected plot 1
  - selected Basil seed packet
  - clicked Plant Selected
  - verified plot 1 entered `tilling` with `queuedCropId: "basil"`

## Cleanup Performed
No temporary source files were created. The first debug screenshot is retained as evidence because it was part of the browser boot diagnostic.

## Risks
The seed packet text is intentionally still runtime text and may need another tuning pass for larger/clearer labels after user visual review.

The `seed_packet_empty` art includes the same small token motif as other packet art; if that reads as a real seed rather than an empty slot, it should be adjusted in the next art pass.

## Memory-Worthy Notes
The seed bag is now asset-backed and no longer purely Phaser rectangle placeholder UI.

The clean alpha crop path is the correct install source for this UI set; the magenta-bounds preview was only a guide and should not be used as runtime art.

## Do Not Promote To Memory
Do not mark the seed bag UI as final approved art until the user reviews the in-engine screenshot.

## Next Recommended Gate
User visual review of `garden-seed-bag-ui-wired-1280x720.png`; then tune label size/spacing or empty-slot art if needed.
