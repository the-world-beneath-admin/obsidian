# TWB Trenchworks Scout Cutout And Patrol Corporal Source Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D, war-side unit sprite pipeline.

## What Changed

- Promoted `war-unit-scout-v2` candidate 01 sheets to accepted source sheets after user approval.
- Cleaned the scout sheets using the established three-sweep cyan process:
  1. exterior cyan flood/background removal,
  2. cyan-family fringe removal,
  3. interior cyan spot cleanup.
- Produced five normalized transparent scout sheets and `80` cut `128 x 128` frames.
- Generated `war-unit-patrol-corporal-v2` candidate 01 source sheets for review:
  - move,
  - crouch,
  - crawl,
  - primary carbine fire,
  - secondary command flare/whistle/rally signal.
- Updated the v2 unit-sheet index.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sheets-v2-index.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-scout-v2-cutout-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-scout-v2-transparent-cutout-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-patrol-corporal-v2-candidate-01-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-patrol-corporal-v2-candidate-01-review-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Cutouts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Move\war-unit-patrol-corporal-v2-move-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Crouch\war-unit-patrol-corporal-v2-crouch-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Crawl\war-unit-patrol-corporal-v2-crawl-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Primary\war-unit-patrol-corporal-v2-primary-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Secondary\war-unit-patrol-corporal-v2-secondary-candidate-01-source-cyan.png`

## Tests And Checks Run

- Verified scout output includes five transparent sheets.
- Verified scout frame cutout count: `80`.
- Verified scout transparent sheet corner alpha values are all `0`.
- Verified no remaining cyan-family opaque pixels under the cleanup threshold.
- Created visual preview sheets for scout cutout and Patrol Corporal candidate 01.
- Unity compile was not run; this pass only added/processed art assets and docs.

## Cleanup Performed

- No scratch files were left in the project tree.
- Original generated images under Codex's generated-image folder were preserved; project copies were made under the Trenchworks asset tree.

## Risks

- Patrol Corporal candidate 01 is not accepted or cut yet.
- Patrol Corporal is a command unit intended for `128 x 256` frames. Candidate 01 has readable command gear and actions, but should be reviewed for whether the silhouette is tall/distinct enough before acceptance.
- If command units must be visually much larger than standard units, regenerate Patrol Corporal with a stronger tall-frame composition before cutting.

## Memory-Worthy Notes

- Scout is now the second approved/cut standard soldier after Rifleman.
- The three-sweep cyan process continues to validate cleanly.
- Command units need a stricter visual gate than standard soldiers because their gameplay footprint and frame height are different.

## Follow-Up Recommendations

- User should review `war-unit-patrol-corporal-v2-candidate-01-review-contact-sheet.png`.
- If Patrol Corporal is approved, promote to accepted and cut using a command-frame-aware process.
- If Patrol Corporal is too similar in height to regular troops, regenerate before any cutout work.

## Anything Blocked

- Patrol Corporal cutout is intentionally blocked on user review.
