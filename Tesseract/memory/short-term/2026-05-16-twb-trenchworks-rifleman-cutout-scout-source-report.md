# TWB Trenchworks Rifleman Cutout And Scout Source Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D, war-side unit sprite pipeline.

## What Changed

- Cleaned the accepted `war-unit-rifleman-v2` cyan source sheets using the requested three-sweep process:
  1. exterior cyan flood/background removal,
  2. near-cyan/darker cyan fringe removal,
  3. interior cyan spot cleanup.
- Produced five normalized transparent rifleman sheets at `512 x 512`.
- Cut the rifleman into `80` transparent `128 x 128` frame PNGs.
- Generated five `war-unit-scout-v2` candidate source sheets for review:
  - move,
  - crouch,
  - crawl,
  - primary carbine fire,
  - secondary binoculars/scout lamp.
- Updated the v2 unit-sheet index with rifleman cutout status and scout review candidate paths.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sheets-v2-index.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-cutout-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-transparent-cutout-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-scout-v2-candidate-01-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-scout-v2-candidate-01-review-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Cutouts\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Move\war-unit-scout-v2-move-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Crouch\war-unit-scout-v2-crouch-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Crawl\war-unit-scout-v2-crawl-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Primary\war-unit-scout-v2-primary-candidate-01-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Source\Secondary\war-unit-scout-v2-secondary-candidate-01-source-cyan.png`

## Tests And Checks Run

- Verified all five rifleman transparent sheets are `512 x 512`.
- Verified each rifleman source sheet produced `16` frame cutouts.
- Verified total rifleman cutout count: `80` frames.
- Verified transparent sheet corner alpha values are all `0`.
- Verified no remaining cyan-family opaque pixels under the cleanup threshold.
- Created visual preview contact sheets for rifleman transparent output and scout candidates.
- Unity compile was not run because this pass only added/processed art assets and docs.

## Cleanup Performed

- No throwaway scratch files were left in the project tree.
- Original generated images under Codex's generated-image folder were preserved; project copies were placed under the Trenchworks asset tree.

## Risks

- Scout sheets are candidates only; they have not been accepted, cleaned, cut, or wired into Unity.
- The scout primary and secondary sheets should be reviewed for direction readability before accepting.
- Generated source sheets remain `1254 x 1254`; final sheet normalization should happen only after approval.

## Memory-Worthy Notes

- The three-sweep cyan cleanup worked cleanly again on the approved rifleman sheets.
- Preserve this cutout rule for future war-side sprite work: exterior cyan, near-cyan fringe, interior cyan.
- Use five sheet types per standard soldier for now: move, crouch, crawl, primary, secondary.
- Do not cut candidate soldier sheets before user visual approval.

## Follow-Up Recommendations

- User should review `war-unit-scout-v2-candidate-01-review-contact-sheet.png`.
- If approved, move scout candidate sheets to `Accepted`, then run the same three-sweep cleanup and `128 x 128` frame cutout process.
- Continue the production order with `war-unit-patrol-corporal-v2` only after scout is accepted or rejected.

## Anything Blocked

- No blockers for rifleman cutouts.
- Scout cutout is intentionally blocked on user review.
