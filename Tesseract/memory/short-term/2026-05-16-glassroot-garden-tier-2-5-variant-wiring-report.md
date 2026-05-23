# Glassroot Garden Tier 2-5 Variant Wiring Report

## Scope

- World Key: The Garden / Glassroot Garden.
- Project: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Task: wire level/tier 2-5 visual variants for plots, well, and compost heap using existing approved local cutouts only.

## What Changed

- Added tiered texture manifests for plot beds, well, compost heap base, and compost fill mound in `src\scenes\GlassrootGardenScene.ts`.
- Added runtime tier-visual refresh logic driven by `getUnlockedGardenTier()`.
- Plot, well, compost base, and compost fill visuals now swap to the highest available unlocked tier texture, with fallback down to lower tiers if a texture is missing.
- Kept existing footprints and hit areas stable by preserving current display sizes and positions.
- Preserved existing plot highlight, plot-selection sparkles, well water sparkle emitter, compost fill mask animation, compost smell wisps, pet selector, companion, signpost, and door animation behavior.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-plot-tier-5.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-well-tier-5.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\garden-compost-tier-5.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-2.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-3.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-4.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\compost-fill-mound-tier-5.png`

`npm run build` also refreshed `dist\`.

## Assets Installed

Source folder:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\ground-progression-sheet-01\crops`

- Plot tiers: `051-cutout.png`, `059-cutout.png`, `067-cutout.png`, `075-cutout.png` installed as tiers 2-5.
- Compost heap base tiers: `056-cutout.png`, `064-cutout.png`, `072-cutout.png`, `079-cutout.png` installed as tiers 2-5.
- Compost fill tiers: `057-cutout.png`, `065-cutout.png`, `073-cutout.png`, `081-cutout.png` installed as tiers 2-5.
- Well tiers: `090-cutout.png`, `089-cutout.png`, `086-cutout.png`, `083-cutout.png` installed as tiers 2-5.

No required tier 2-5 plot, well, compost base, or compost fill assets were missing from the accepted local cutout sheet.

## Tests And Checks

- `npm run build` from `C:\Users\yrred\Desktop\Unity\TWB-Farming`: passed.
- Build retained the existing Vite warning that some chunks exceed 500 kB after minification.
- Playwright viewport screenshot captured at 1280x720 after granting test XP to Tier 5 through the existing debug hook.

## Screenshot

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\garden-tier-5-variants-1280x720.png`

## Cleanup Performed

- Closed the temporary Playwright browser session.
- No source files, reports, raw evidence, or unrelated project files were deleted.
- No git staging, commits, resets, or broad cleanup were performed.

## Risks

- The tiered well art has taller source dimensions than tier 1, but it is constrained to the existing well footprint to avoid moving service points or hit areas. Live review should decide whether higher-tier wells need a tuned display height/anchor.
- Compost fill uses matching tiered mound art, but the existing mask dimensions remain shared across tiers. It behaves correctly in the screenshot, but live fill-level review should still inspect tiers 2-5.
- Plot tier variants are mapped from the first plot-bed cutout in each progression row of the approved sheet. That matches the installed tier 1 pattern, but final art-direction acceptance should confirm the chosen row/column variants.
- `TWB-Farming` is not a git repository, so file status could not be checked with `git status`.

## Memory-Worthy Notes

- Existing approved cutouts from `ground-progression-sheet-01` cover tier 2-5 plot, well, compost heap, and compost fill variants.
- Runtime tier art should remain keyed to `getUnlockedGardenTier()` unless design later separates plot/well/compost upgrade levels from overall Garden tier.

## Follow-Up Recommendations

- Live browser review should inspect tier 2, 3, 4, and 5 specifically, not only Tier 5.
- Consider adding an explicit debug control for setting Garden tier without awarding XP if repeated visual QA continues.
