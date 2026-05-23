# Glassroot Garden Seed Bag Tier Tabs Report

## Task

Improve the Garden seed bag UI so seed-slot text is readable, seed cards show only the seed image plus plant name, and the bag is split into tier tabs instead of cramped pagination.

## Result

Completed. The seed bag now uses the existing parchment/panel assets with a larger tier-tab layout:

- Panel moved/reframed to gain usable space: right/bottom edge moved down/right while the top-left area expands slightly into the playfield.
- Seed packet grid changed from 3 x 3 paged slots to 2 x 3 tier slots.
- Tier tabs `T1` through `T5` replace Prev/Next paging.
- Seed cards now show only the seed sprite and plant name.
- Removed the small `T1 tap` / `Filler tap` text from seed cards.
- `Plant Selected` button is larger and easier to read.
- `Comfreygrass` wraps as `Comfrey` / `grass` to fit the new card.

## Whether The Plant/Bar Artifact Was Reproduced

Not reproduced during this clean Playwright check. The screenshot showed empty plots without the earlier all-plot mature plant / blue-bar artifact.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-glassroot-garden-seed-bag-tier-tabs-report.md`

## Assets Converted Or Explicitly Not Converted

No new assets were generated or converted. This pass reused the existing seed bag panel, close button, seed packet, and action button PNGs.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-seed-bag-tier-tabs-1280x720.png`

## Checks Run

- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming` - passed.
- Playwright clean browser check at `http://127.0.0.1:5173/` with a 1280 x 720 screenshot - passed.

## Cleanup Performed

No throwaway source files were created. The screenshot was intentionally kept as visual evidence. `npm run build` refreshed Vite build output in `dist`.

## Risks

- Locked tier tabs are intentionally dim; live review should confirm they are not too dim on the user's monitor.
- Higher-tier cards have fewer than six crops, so empty packet slots remain visible for consistency.

## Memory-Worthy Notes

- The tier-tab seed bag layout is a stronger direction than the 3 x 3 paged bag for readability.
- Future seed bag art should preserve a 2-column card layout, not return to small dense packet buttons.

## Do Not Promote To Memory

- The exact pixel offsets may still be tuned after live visual review.

## Next Recommended Gate

Live browser review of the seed bag at `http://127.0.0.1:5173/`, especially the `T1` tab readability, card spacing, and whether locked tabs need more contrast.
