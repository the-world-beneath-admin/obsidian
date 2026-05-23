# Glassroot Garden Seed Bag Icon Fit Report

## Task

Tune seed image placement inside the new seed bag cards so the seed sprites are smaller and centered in the packet icon box.

## Result

Completed. The seed icons now target the small raised box in the upper-left of each seed packet instead of the broader packet area.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-seed-bag-icon-fit-report.md`

## Assets Converted Or Explicitly Not Converted

No assets were generated, converted, or edited. This was a runtime placement/scale adjustment only.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-seed-bag-icons-centered-1280x720.png`

## Checks Run

- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming` - passed.
- Playwright screenshot at 1280 x 720 - passed.

## Cleanup Performed

No temporary scratch files were created. Screenshot retained as visual evidence.

## Risks

- Icons are now contained in the packet frame, but live review should decide whether they can be enlarged slightly while still staying inside the small box.

## Memory-Worthy Notes

- Seed packet icons should be anchored to the packet's small upper-left raised box, not the whole left side of the card.

## Do Not Promote To Memory

- Exact icon offsets and max dimensions are still visual-tuning values.

## Next Recommended Gate

Live review of the seed bag in the user's browser to decide whether the icon size should be increased slightly after this centering pass.
