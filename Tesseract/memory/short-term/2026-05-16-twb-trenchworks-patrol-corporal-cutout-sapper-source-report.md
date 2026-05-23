# TWB Trenchworks Patrol Corporal Cutout And Sapper Source Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D, war-side unit sprite pipeline.

## What Changed

- Promoted `war-unit-patrol-corporal-v2` candidate 01 sheets to accepted source sheets after user approval.
- Cleaned Patrol Corporal with the established three-sweep cyan process:
  1. exterior cyan flood/background removal,
  2. cyan-family fringe removal,
  3. interior cyan spot cleanup.
- Produced five normalized transparent Patrol Corporal command sheets at `512 x 1024`.
- Cut Patrol Corporal into `80` transparent `128 x 256` command-frame PNGs.
- Generated `war-unit-sapper-v2` candidate 01 source sheets for review:
  - move,
  - crouch,
  - crawl,
  - primary short-rifle fire,
  - secondary shovel/trench-tool action.
- Updated the v2 unit-sheet index.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sheets-v2-index.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-patrol-corporal-v2-cutout-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-patrol-corporal-v2-transparent-cutout-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sapper-v2-candidate-01-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sapper-v2-candidate-01-review-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Cutouts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Move\war-unit-sapper-v2-move-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Crouch\war-unit-sapper-v2-crouch-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Crawl\war-unit-sapper-v2-crawl-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Primary\war-unit-sapper-v2-primary-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Secondary\war-unit-sapper-v2-secondary-candidate-01-source-cyan.png`

## Tests And Checks Run

- Verified Patrol Corporal output includes five transparent sheets.
- Verified Patrol Corporal frame cutout count: `80`.
- Verified Patrol Corporal transparent sheet corner alpha values are all `0`.
- Verified no remaining cyan-family opaque pixels under the cleanup threshold.
- Created visual preview sheets for Patrol Corporal cutout and Sapper candidate 01.
- Unity compile was not run; this pass only added/processed art assets and docs.

## Cleanup Performed

- No scratch files were left in the project tree.
- Original generated images under Codex's generated-image folder were preserved; project copies were made under the Trenchworks asset tree.

## Risks

- Sapper candidate 01 is not accepted or cut yet.
- Patrol Corporal source was generated on a square sheet, then normalized into `128 x 256` command frames without stretching. This is mechanically correct, but the art still depends on the approved candidate's natural command silhouette.
- Sapper secondary action is strong visually; user should still confirm direction readability before approval.

## Memory-Worthy Notes

- First command unit cutout path is now proven: `512 x 1024` transparent sheets, `128 x 256` frames, aspect preserved and bottom-aligned.
- Standard soldier queue continues as five sheets per unit: move, crouch, crawl, primary, secondary.
- Keep the Sapper identity centred on shovel/trench-tool work, not generic engineering machinery.

## Follow-Up Recommendations

- User should review `war-unit-sapper-v2-candidate-01-review-contact-sheet.png`.
- If Sapper is approved, promote to accepted and cut as standard `128 x 128` frames.
- Next queued unit after Sapper is `war-unit-combat-medic-v2`.

## Anything Blocked

- Sapper cutout is intentionally blocked on user review.
