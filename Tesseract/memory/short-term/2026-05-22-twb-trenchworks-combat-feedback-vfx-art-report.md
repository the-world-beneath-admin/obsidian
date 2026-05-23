# TWB Trenchworks Combat Feedback VFX Art Report

Date: 2026-05-22

## Scope

Standalone TWB-tagged Unity 2D game: TWB Trenchworks.

This pass created the next war-side art batch: first-pass world-space combat feedback / burst VFX. It did not modify the raw GPT Pro package, permanent Obsidian wiki memory, or unrelated TWB projects.

## What Changed

- Created `CombatFeedback/V1` under the live Trenchworks Unity project.
- Generated 14 combat-feedback effects:
  - rifle muzzle
  - MG muzzle
  - mortar launch
  - bullet tracer
  - grenade burst
  - artillery impact
  - dirt impact
  - sandbag hit
  - metal spark
  - smoke puff
  - fire puff
  - suppression marker
  - casualty marker
  - bombardment warning
- Exported 56 transparent 128x128 frame PNGs.
- Exported 14 horizontal 512x128 strip PNGs for runtime import experiments.
- Exported a manifest with first-pass anchor, canvas, alpha, and usage metadata.
- Exported review/contact sheets for visual inspection.
- Packaged the batch as `C:\Users\yrred\Downloads\twb-trenchworks-combat-feedback-v1.zip`.
- Updated the Trenchworks art catalog and active task brief to record this as VFX/combat feedback art, not as solid assets or completed runtime integration.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_combat_feedback_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\VFX\CombatFeedback\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\combat-feedback-v1\`
- `C:\Users\yrred\Downloads\twb-trenchworks-combat-feedback-v1.zip`

## Review Images

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\combat-feedback-v1\combat-feedback-v1-frame1-examples.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\combat-feedback-v1\combat-feedback-v1-contact-sheet.png`

## Child QA

Child reviewer Locke (`019e5297-fb41-7093-b64e-3a6e85fb6151`) audited the proposed pack as a read-only execution child.

Key result:

- The pack fills a real catalog gap if treated as runtime burst VFX.
- Existing older sheets overlap with some effects, so this pack must be documented as world-space combat feedback with anchors/timing/LOD intent.
- The reviewer recommended adding clearer artillery or tracer feedback. The final generator expanded from 12 to 14 effects by adding `bullet-tracer` and `artillery-impact`.
- Suppression and casualty markers should remain temporary world-space combat feedback and not be confused with final HUD/status icons.

## Checks Run

- Regenerated VFX pack with:
  - `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_combat_feedback_v1.py`
- Mechanical sprite QA:
  - Frame PNG count: 56 / expected 56.
  - Strip PNG count: 14 / expected 14.
  - Frame dimensions: 128x128.
  - Strip dimensions: 512x128.
  - Bad alpha/dimension sample count: 0.
- Zip QA:
  - Zip entries: 75.
  - Frame PNGs in zip: 56.
  - Strip PNGs in zip: 14.
  - Manifest included: yes.
  - Generator included: yes.
- Visual review:
  - Opened frame-1 examples sheet.
  - Opened full contact sheet.

## Cleanup Performed

- No scratch files were created outside the intended asset, review, docs, and package outputs.
- No source files were deleted.
- No raw GPT Pro package files were modified.

## Risks

- Unity emitter/socket validation was not run.
- Effects are not yet wired to combat, soldier weapons, emplacements, bombardment, or camera zoom LOD.
- First-pass anchors in the manifest must be checked against live soldier, weapon, and emplacement muzzle/impact positions.
- Suppression/casualty marker effects could visually collide with final HUD/status marker language unless kept as temporary world-space feedback.
- Some effects overlap older VFX sheets, but this pack is better structured for runtime burst frames and explicit anchors.

## Memory-Worthy Notes

- Combat feedback should be treated as a separate art category from solid assets and decoration assets.
- VFX acceptance needs a runtime emitter proof: anchor placement, sorting, burst timing, zoomed-out readability, and distinction from UI/status icons.
- A useful next VFX gate is to wire a small subset first: rifle muzzle, MG muzzle, bullet tracer, dirt impact, and artillery impact.

## Follow-Up Recommendations

- Run a narrow Unity integration slice for 5 effects before expanding the whole pack into the combat renderer.
- Keep `CombatFeedback/V1` in the catalog as first-pass art until live emitter proof passes.
- Next art batch can return to war-side missing categories such as projectile/world-space decals, terrain damage overlays, or build/repair feedback.
