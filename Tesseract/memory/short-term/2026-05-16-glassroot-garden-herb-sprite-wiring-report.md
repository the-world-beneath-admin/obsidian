# 2026-05-16 Glassroot Garden Herb Sprite Wiring Report

## Task
Wire the QC-clean herb/plant production sprite sheets into Glassroot Garden, including plot growth visuals, seed-bag icons, storage/drying/bin visuals, and pet seed-carry planting behaviour.

## Result
Complete. The Garden scene now loads the cleaned plant sprite assets from source assets, uses them for plot growth stages, seed packets, raw/dried storage bins, drying rack bundles, and finished bundle shelf accents. Pets now attach a small seed sprite after visiting the tool shed and drop it into the selected plot before the crop is committed.

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herb-sprites-wired-1280x720.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herb-storage-sprites-wired-1280x720.png`

## Assets Converted Or Installed
Installed the QC-clean transparent plant cells from:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\plant-production-sprite-prompts\cutout-cells\`

into:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\plants\`

Installed 21 plant folders with 8 sprite stages each: `seed-planted`, `sprout`, `mature`, `ready-harvest`, `raw-bin`, `drying-undried`, `drying-dried`, and `dry-bundle`.

No new image generation was performed in this pass.

## Screenshots Captured
- Main Garden seeded visual proof: `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herb-sprites-wired-1280x720.png`
- Storage room seeded visual proof: `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-herb-storage-sprites-wired-1280x720.png`

## Checks Run
- `npm run build` passed.
- Local dev server started at `http://127.0.0.1:5173/`.
- In-app browser UI path was used to queue a real planting; the seed sprite appeared in the bed after planting.
- Headless Playwright screenshot pass succeeded with SwiftShader WebGL args and reported no page errors.

## Cleanup Performed
- Removed the temporary SwiftShader probe screenshot after confirming headless rendering worked.
- Dev server stdout/stderr logs remain under `output\playwright\` because the dev server is still running for user review.

## Risks
- The full 21-plant production sprite set increases shipped asset volume substantially; Vite still builds, but the large chunk warning remains and asset size should be revisited before shipping.
- Ready crops can auto-harvest quickly in seeded proof captures, so screenshots may show harvesting overlays even when the sprite wiring is working.
- Plot-stage sprite sizes are first-pass fitted to the current Tier 1 bed footprint; later tiers or taller plant silhouettes may need per-crop tuning.

## Memory-Worthy Notes
- Plant assets are now source-installed under `src\assets\glassroot\garden\plants\<cropId>\`.
- Runtime plant loading uses Vite `import.meta.glob` so new same-named stage files under those crop folders will be included automatically.
- Pet planting now has a distinct seed carry/drop moment instead of instantly committing the crop at arrival.

## Do Not Promote To Memory
- The seeded screenshot state is only a verification setup, not a gameplay balance decision.
- Current plot sprite sizing is provisional and should not be treated as final art direction.

## Next Recommended Gate
Live review in the user browser: watch one full plant job from tool shed seed pickup to plot drop, then inspect one harvested crop entering the herbalist storage flow.
