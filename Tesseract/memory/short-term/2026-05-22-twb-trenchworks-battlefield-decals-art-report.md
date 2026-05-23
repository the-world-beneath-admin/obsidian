# TWB Trenchworks Battlefield Decals Art Report

Date: 2026-05-22

## Scope

Standalone TWB-tagged Unity 2D game: TWB Trenchworks.

This pass created the next war-side art batch: persistent battlefield terrain damage, aftermath, construction, repair, and hardpoint damage overlays. It did not modify the raw GPT Pro package, permanent Obsidian wiki memory, or unrelated TWB projects.

## What Changed

- Created `BattlefieldDecals/V1` under the live Trenchworks Unity project.
- Generated 18 persistent overlay decal families:
  - fresh shell crater
  - old dry shell crater
  - scorched blast mark
  - dirt spray fan
  - bullet-pocked ground strip
  - sandbag spill
  - broken timber splinters
  - rubble scatter small
  - rubble scatter large
  - mud churn / trampled path
  - flooded mud edge
  - subtle casualty ground mark
  - construction stakes layout
  - under-construction plank patch
  - repair patch: fresh sandbags
  - repair patch: timber bracing
  - damaged hardpoint smoke stain
  - destroyed hardpoint footprint
- Exported 162 transparent 192x192 PNGs:
  - 18 decal families
  - 3 biome tints: desert, temperate forest, tropical jungle
  - 3 severities: light, medium, heavy
- Exported a manifest with placement, footprint, blocking, alpha, biome, and severity metadata.
- Exported one overview sheet and three per-biome contact sheets.
- Packaged the batch as `C:\Users\yrred\Downloads\twb-trenchworks-battlefield-decals-v1.zip`.
- Updated the Trenchworks art catalog and active task brief.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_battlefield_decals_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\VFX\BattlefieldDecals\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\battlefield-decals-v1\`
- `C:\Users\yrred\Downloads\twb-trenchworks-battlefield-decals-v1.zip`

## Review Images

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\battlefield-decals-v1\battlefield-decals-v1-medium-examples.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\battlefield-decals-v1\battlefield-decals-v1-desert-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\battlefield-decals-v1\battlefield-decals-v1-temperate-forest-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\battlefield-decals-v1\battlefield-decals-v1-tropical-jungle-contact-sheet.png`

## Child QA

Child reviewer Sagan (`019e52a0-e070-7250-bc32-f5dc8110c7ed`) audited the next-batch choice as a read-only execution child.

Key result:

- The next best gap after `CombatFeedback/V1` was persistent battlefield decals / terrain damage / build-repair feedback.
- The reviewer recommended the exact categories that this generator now covers: craters, scorch, dirt spray, bullet-pocked ground, sandbag spill, timber/rubble, mud/flooding, casualty ground mark, construction layout, plank patch, repair patches, smoke stain, and destroyed hardpoint footprint.
- Runtime risks called out: sorting, pooling/stack caps, zoom readability, and keeping decals non-blocking/non-targetable unless a later gameplay system explicitly binds them to hazards.

## Checks Run

- Regenerated decal pack with:
  - `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_battlefield_decals_v1.py`
- Mechanical sprite QA:
  - Decal PNG count: 162 / expected 162.
  - Dimensions: 192x192.
  - Bad alpha/dimension sample count: 0.
- Zip QA:
  - Zip entries: 169.
  - Decal PNGs in zip: 162.
  - Review PNGs in zip: 4.
  - Manifest included: yes.
  - Generator included: yes.
- Visual review:
  - Opened medium examples sheet.
  - Opened temperate forest contact sheet.

## Cleanup Performed

- The generator removes stale `.png`, `.json`, and `.md` outputs in its own dedicated output and review folders before regenerating, preventing old decal names from lingering.
- No source files were deleted outside the intended BattlefieldDecals V1 output/review folders.
- No raw GPT Pro package files were modified.
- Child worker was closed after review.

## Risks

- Unity overlay validation was not run.
- Sorting must be proven: above ground, below soldiers, and usually below hardpoint structures except explicit damage overlays.
- Runtime needs pooling/stacking caps so persistent decals do not recreate the performance drag problem.
- Some decals are intentionally subtle; zoomed-out readability still needs a live camera check.
- These are non-blocking visual overlays in the manifest. If later systems make them hazards, the gameplay meaning must be explicit.

## Memory-Worthy Notes

- Combat feedback now has two distinct categories:
  - `CombatFeedback/V1`: burst/animated event feedback.
  - `BattlefieldDecals/V1`: persistent or semi-persistent ground/build/repair aftermath overlays.
- The next art-kit gap should likely move to either projectile/throwable iconography, emplacement operation overlays, or war-side decoration assets once solid and feedback layers are considered adequate.

## Follow-Up Recommendations

- Runtime-test a small overlay slice with shelling terrain, hardpoint damage, and construction/repair progress.
- Add a decal manager/pool before allowing frequent combat events to spawn persistent overlays.
- Keep this pack cataloged as first-pass art until Unity sorting, lifetime, pooling, and readability validation pass.
