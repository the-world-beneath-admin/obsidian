# Main Game Kickstarter System Screenshot Report - 2026-05-22

## Scope

- Lane: Main game / The World Beneath.
- Goal: capture clean, frame-only screenshots of implemented main-game systems for Kickstarter preparation.

## What changed

- Added an Editor-only capture runner at `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\KickstarterFrameCaptureRunner.cs`.
- The runner opens `Assets/Scenes/IdleTestScene.unity`, enters Play Mode, seeds a dev-only proof inventory, stages crafting selections, arranges the portrait UI windows in-frame, captures screenshots, writes a manifest, and exits Unity.
- Screenshot fixture seeds:
  - pet/archive cards: Chuck, Peggy, Stanly, Nova plus skill/modifier cards;
  - materials/assets: Will, elemental essences, low/iron/high materials;
  - Craft Create: three active material slots;
  - Craft Apply: selected Peggy companion card plus modifier slots.

## Outputs

Raw screenshot folder:

`C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\raw\launch\kickstarter\2026-05-22\main-game-system-screenshots`

Captured frames:

- `01-phone-home.png`
- `02-archive-cards.png`
- `03-inventory-assets.png`
- `04-craft-create-staged.png`
- `05-craft-apply-staged.png`
- `06-activities-world-map.png`
- `07-recipes.png`
- `08-settings.png`

Supporting files:

- `manifest.md`
- `unity-capture-final.log`

## Verification

- Unity visible-editor capture run completed and exited on its own.
- All eight screenshots are present at `1080x1920`.
- Visual spot-check confirmed:
  - Archive shows visible pet cards.
  - Inventory shows material/card asset state.
  - Craft Create has active material cards.
  - Craft Apply has a selected companion and modifier cards.
- Unity log shows all eight `KickstarterFrameCaptureRunner` captures completed.

## Cleanup

- Removed failed intermediate capture logs from the screenshot folder.
- Kept only `unity-capture-final.log` as the final evidence log.

## Risks / Notes

- The screenshots are portrait because the current UI is phone/manifest oriented. This is correct for showing the implemented UI cleanly, but Kickstarter page layout may still want cropped landscape composites later.
- The runner is Editor-only and dev-fixture based; it does not alter live balance or player persistence.
- No permanent wiki/index/hot memory was promoted from this pass.

## Next recommended gate

Select the strongest 3-5 frames for the Kickstarter page, then make cropped or composited marketing-ready exports while preserving these raw captures as evidence.
