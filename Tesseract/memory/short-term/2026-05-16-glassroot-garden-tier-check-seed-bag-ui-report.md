# 2026-05-16 Glassroot Garden Tier Check Seed Bag UI Report

## Task
Verify whether all 5 well and compost levels are wired in Glassroot Garden. If confirmed, generate a proper source asset sheet for replacing the placeholder seed bag UI.

## Result
Confirmed all 5 well tiers and all 5 compost heap tiers are wired in `GlassrootGardenScene.ts`.

The scene also has tiered compost-fill mound support for tiers 1-5. Tier 1 uses `compost-fill-mound.png`; tiers 2-5 use `compost-fill-mound-tier-2.png` through `compost-fill-mound-tier-5.png`.

Generated a new local cyan-matte seed bag UI source set under:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\`

## Files Touched
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\seed-bag-ui-set-source.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\seed-bag-ui-set-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\seed-bag-ui-set-manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\seed-bag-ui-set-guide.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\crops\*.png`

No source code was modified.

## Assets Converted Or Generated
Generated one seed bag UI source sheet locally with no external image generation:

- Full seed bag panel backing
- Header/footer plaques
- Close button states
- Seed packet states: normal, hover, selected, locked, empty
- Small nav button states
- Plant Selected button states
- Page badges
- Seed tokens
- Divider trim
- Optional 3x3 slot grid backing
- 40 individual component crops exported from the sheet

## Wiring Confirmed
`GlassrootGardenScene.ts` contains explicit tier maps for:

- `GARDEN_WELL_TEXTURES`: tiers 1-5
- `GARDEN_COMPOST_TEXTURES`: tiers 1-5
- `COMPOST_FILL_MOUND_TEXTURES`: tiers 1-5

The assets are preloaded from these maps and refreshed through `refreshGardenTierVisuals()`, using `getUnlockedGardenTier()` and `getTieredGardenTextureKey()`.

## Screenshots Or Previews
No browser screenshot was captured because no runtime visual code changed.

Generated preview:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\output\asset-conversion\garden-main-screen\seed-bag-ui-set-01\seed-bag-ui-set-preview.png`

## Checks Run
- Inspected tier texture maps in `GlassrootGardenScene.ts`.
- Confirmed asset files exist for all well tiers 1-5.
- Confirmed asset files exist for all compost tiers 1-5.
- Confirmed compost fill mound files exist for tier 1 plus tiers 2-5.
- Seed bag UI sheet QC: near-cyan fringe threshold scan returned `0`.
- `npm run build` passed.

## Cleanup Performed
Regenerated the seed bag sheet after identifying off-cyan shadow fringes in the first pass. The final source sheet intentionally omits external drop shadows to avoid cyan matte contamination.

## Risks
The seed bag UI asset sheet is not wired into the live game yet. Current runtime seed bag is still Phaser-drawn placeholder rectangles and text.

The generated UI set is procedural art, not hand-painted. It is clean and cut-ready, but it may need one visual approval pass before installation.

## Memory-Worthy Notes
Well, compost heap, and compost fill mound tier visuals are already wired for Garden tiers 1-5.

The seed bag remains the last obvious placeholder surface on screen one.

For cyan-matte source assets, avoid external shadows on the cyan background because they create off-cyan halo pixels that later require cleanup.

## Do Not Promote To Memory
Do not promote the procedural seed bag UI set as final approved art until the user approves the preview and it is wired into the runtime.

## Next Recommended Gate
Review `seed-bag-ui-set-preview.png`. If approved, wire the component crops into `renderSeedBag()`, replacing the current rectangle placeholders while keeping labels, page counts, tier text, crop names, and button labels as runtime Phaser text.
