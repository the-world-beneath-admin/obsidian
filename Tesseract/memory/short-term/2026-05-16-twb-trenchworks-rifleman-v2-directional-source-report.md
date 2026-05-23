# TWB Trenchworks Rifleman v2 Directional Source Report

Date: 2026-05-16
Worker: TWB Trenchworks playtest/asset worker
Scope: TWB Trenchworks standalone Unity 2D, war-side rifleman source sheets.

## What Changed

- Corrected the soldier sheet plan from one all-purpose side-facing sheet to directional production sheets.
- Documented the v2 directional batching contract.
- Moved the deprecated v1 placeholder sheets out of the active source lane without deleting them.
- Copied the approved soldier reference into the Unity asset tree.
- Generated and accepted the first rifleman v2 directional source set:
  - movement
  - crouch
  - crawl
  - primary rifle fire
  - secondary grenade action
- Rejected the first combined low-posture sheet because it did not clearly separate left/right crouch direction.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-directional-batching-v2.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sheets-v2-index.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sheets-v2-briefs.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-squad-unit-animation-contract-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trenchworks-war-asset-output-index-v1.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-move-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-low-candidate-01-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-crouch-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-crawl-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-primary-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-rifleman-v2-secondary-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Reference\war-soldier-style-reference-v1.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\Move\war-unit-rifleman-v2-move-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\Crouch\war-unit-rifleman-v2-crouch-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\Crawl\war-unit-rifleman-v2-crawl-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\Primary\war-unit-rifleman-v2-primary-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\Secondary\war-unit-rifleman-v2-secondary-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\DeprecatedPlaceholderV1\`

## Tests And Checks Run

- Visually checked each accepted rifleman v2 sheet for:
  - approved trench soldier style
  - no blob/South-Park placeholder look
  - readable down/left/right/up facings
  - no text, labels, UI, or watermark
  - no cropped weapons or limbs
- Checked each accepted source image dimensions and sampled corner colors.
- Confirmed `5` accepted rifleman v2 source sheets exist.

## Cleanup Performed

- Deprecated v1 placeholder sheets were moved out of active `Sheets\Source`, `Sheets\Transparent`, and `Frames` folders into `Assets\Art\War\Units\DeprecatedPlaceholderV1\`.
- No generated raw image evidence under `.codex\generated_images` was deleted.

## Risks

- Accepted source sheets are still cyan-matte sources, not cleaned transparent cutouts.
- Generated dimensions are `1254 x 1254`, so the cleanup/cutting pass must normalize them to `512 x 512` with `128 x 128` frames.
- Background is cyan-family rather than exact `#00FFFF`; cleanup should use sampled-border chroma removal.
- Secondary grenade row directions are readable enough for first pass, but should get an extra visual review before cutting.

## Memory-Worthy Notes

- Soldier production now uses directional source sheets rather than one all-purpose sheet.
- First-slice roles should likely follow rifleman batching: movement, crouch, crawl, primary, secondary.
- Combined 8-row low-posture sheets may be too risky for generation; split crouch/crawl is safer.
- Left/right may occasionally be easier to mirror at cut/runtime, but accepted source sheets should still be visually reviewed for directional intent.

## Follow-Up Recommendations

- Review the full rifleman v2 accepted source set before cutting.
- If accepted, build a normalizer/cutter that converts each `1254 x 1254` source sheet into exact `512 x 512` transparent sheets and `128 x 128` frames.
- After rifleman cuts pass QA, generate Scout movement next using the same directional batching.

## Blocked

- No blocker for rifleman source generation.
- Cutting is intentionally held until the accepted source set receives review as a group.

