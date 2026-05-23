# Glassroot Garden Notice Bundle Awaiting Guard Report

## Task
Prevent Notice Board quest bundles from being produced multiple times once that order has already been queued into the finished bundle rack, while preserving repeatable transfer bundle production.

## Result
Implemented a Notice Board order availability guard in `GlassrootGardenScene.ts`.

- Notice Board recipes now report unavailable when the same recipe is already active on the finished bundle rack.
- Notice Board recipes now report unavailable after that order has completed once.
- The Notice Board card labels show `Awaiting completion`, `Complete`, or `Open`.
- The Bundler panel shows `Awaiting completion` and a blocked bundle button for unavailable quest orders.
- Finished quest bundles display as `Board Awaiting` on the finished bundle rack.
- Transfer bundles remain repeatable and were verified by queuing two Basil transfer bundles.

## Whether The Plant/Bar Artifact Was Reproduced
Not part of this narrow follow-up. No new investigation was performed on the earlier main-garden plant/bar artifact.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-17-glassroot-garden-notice-bundle-awaiting-guard-report.md`

## Assets Converted Or Explicitly Not Converted
No assets were converted or generated.

## Screenshots Captured
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\notice-bundle-awaiting-guard-1280x720.png`

## Checks Run
- `npm run build` in `C:\Users\yrred\Desktop\Unity\TWB-Farming` passed.
- Playwright browser check at `http://127.0.0.1:5173/`:
  - Queued `notice_greenward_bundle` once.
  - Attempted the same notice bundle again; count remained `1` and event text said it was already awaiting completion.
  - Queued `transfer_basil` twice; count reached `2`.

## Cleanup Performed
No temporary source files were created. The screenshot was intentionally retained as visual evidence.

## Risks
- The guard blocks Notice Board orders permanently after one completion. This matches the current request, but future repeatable quest-board design would need an explicit reset/new-order rotation.
- Existing saved games with a queued notice bundle will now show that order as awaiting and block duplicate production, which is intended.

## Memory-Worthy Notes
- Notice Board bundles are now treated as one-off quest orders: open, awaiting completion, then complete.
- Transfer bundles remain the repeatable route into World Key shared storage.

## Do Not Promote To Memory
Do not promote raw implementation details or temporary test coordinates. Promote only the design rule if accepted: Notice Board quest bundles are one-off orders, transfer bundles are repeatable.

## Next Recommended Gate
Playtest the herbalist room order flow with a real user save after one Notice Board order completes, then decide whether completed orders should disappear, stay marked complete, or rotate into new Notice Board orders later.
