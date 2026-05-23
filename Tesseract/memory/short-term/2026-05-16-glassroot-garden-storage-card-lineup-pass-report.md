# 2026-05-16 Glassroot Garden Storage Card Lineup Pass Report

## Task

Scope: Glassroot Garden World Key / herb drying room UI.

Analyze and fix the raw plant and dried herb summary cards because the cards were still too wide and the text did not align cleanly with the printed ruled lines on the card asset.

## Result

Complete.

Measured the card asset directly. The source card is `196 x 44`; its printed text rules sit around original y `17/18` and `30/31`. The previous display size distorted the card by compressing the height more than the width. The cards now render at `160 x 36`, which is close to the original aspect ratio, and the text/icon/chip anchors were moved to match the asset artwork.

The card text now sits above the printed rules instead of being crossed by them, and the cards are narrower inside the raw/dried storage frames.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`

## Assets Converted

None. Existing cleaned card/panel assets were reused.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\herbalist-room-storage-cards-lineup-pass3-1280x720.png`

## Checks Run

- `npm run build` in `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- Playwright clean-context visual check opened the herb room with seeded raw/dried herbs and captured a 1280 x 720 screenshot.
- Temporary magnified crops were used for visual alignment QA.

## Cleanup Performed

Deleted temporary comparison and magnified crop screenshots from `output\playwright`. Kept only the final pass screenshot.

## Risks

- The cards are now more visually disciplined, but the text is necessarily small because the current panel footprint is tight. If the user wants larger readable labels on mobile, the next correct change is a redesigned larger panel rather than another squeeze pass.

## Memory-Worthy Notes

- Preserve the card artwork aspect ratio when scaling the storage summary cards. The source card is `196 x 44`; the current in-game fit is `160 x 36`.
- The raw/dried storage card text should be positioned as writing above the card's printed rules, not centered through the lines.

## Do Not Promote To Memory

- Test seed quantities used for screenshot setup.

## Next Recommended Gate

Review the final 1280 x 720 screenshot and decide whether the current compact card design is acceptable or whether the storage panel itself should be enlarged/redesigned for a later mobile-first art pass.
