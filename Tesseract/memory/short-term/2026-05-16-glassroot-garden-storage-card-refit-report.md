# 2026-05-16 Glassroot Garden Storage Card Refit Report

## Task

Scope: Glassroot Garden World Key / herb drying room UI.

Redo the raw plant and dried herb storage card area so the summary cards fit properly inside their overall frames without overlapping the footer instructions or compost/action controls.

## Result

Complete.

The card presentation was resized from the earlier oversized `196 x 44` rows to compact `184 x 34` rows with tighter internal icon, text, action chip, and scroll-rail positioning. The panel now reserves a fixed lower footer band for instructions and compost controls, so the three visible summary cards no longer collide with the bottom UI.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`

## Assets Converted

None. Existing cleaned herb room UI assets were reused and scaled in-code.

## Screenshots Captured

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\herbalist-room-storage-cards-refit-1280x720.png`

## Checks Run

- `npm run build` in `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- Playwright clean-context visual check opened the herb room with seeded raw/dried herbs and captured a 1280 x 720 screenshot.

## Cleanup Performed

No temporary script files were created. Inline Playwright was run from the shell only.

## Risks

- The compact cards are intentionally smaller to solve overlap. If the user wants larger touch targets later, the correct next move is a taller or wider redesigned storage panel, not forcing large cards back into the current frame.
- The current panel art is still the previously cleaned cyan-generated UI asset; this pass did not create new bespoke panel art.

## Memory-Worthy Notes

- The herb room storage panels need an explicit internal layout contract: header, fixed-height list viewport, scroll rail, and reserved footer band.
- Three visible rows can fit in the current `220 x 202` panel only if each row is about `34px` tall with compact text and icon placement.

## Do Not Promote To Memory

- The test seed counts used for the screenshot.

## Next Recommended Gate

Review the new screenshot in the live browser and decide whether the storage panels should stay compact or be redesigned as larger mobile-first panels in a future art pass.
