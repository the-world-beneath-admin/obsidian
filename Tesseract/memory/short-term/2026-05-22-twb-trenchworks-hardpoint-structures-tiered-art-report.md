# TWB Trenchworks Hardpoint Structures V1 Tiered Art Report

Date: 2026-05-22
Worker: TWB Trenchworks standing worker
Scope: TWB Trenchworks war-side solid assets

## Summary

Created Hardpoint Structures V1, a tiered hardpoint structure overlay pack designed to sit over/with Hardpoint Pads V1. This continues the war-side art kit and extends the hardpoint upgrade ladder beyond empty pads.

Generated structures:

- MG Nest
- Mortar Emplacement
- Aid Shelter
- Command Dugout

Generated tiers:

- Tier 1 Field Structure
- Tier 2 Reveted Structure
- Tier 3 Reinforced Structure

Generated states:

- Blueprint
- Foundation
- Under Construction
- Active
- Damaged
- Destroyed

Total runtime sprites: 72 transparent 192x192 PNGs.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_hardpoint_structures_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\SolidAssets\HardpointStructures\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\hardpoint-structures-v1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\solid_asset_gameplay_roles_v1.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`

Packaged zip:

- `C:\Users\yrred\Downloads\twb-trenchworks-hardpoint-structures-v1.zip`

## Review Images

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\hardpoint-structures-v1\hardpoint-structures-v1-active-tier-overview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\hardpoint-structures-v1\hardpoint-structures-v1-mg-orientation-check.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\hardpoint-structures-v1\hardpoint-structures-v1-tier1-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\hardpoint-structures-v1\hardpoint-structures-v1-tier2-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\hardpoint-structures-v1\hardpoint-structures-v1-tier3-contact-sheet.png`

## Checks Run

- Ran `generate_hardpoint_structures_v1.py`.
- Verified 72 runtime PNGs were generated.
- Verified all runtime PNGs are 192x192.
- Verified all runtime PNGs have non-empty alpha bounds.
- Visually inspected active tier overview, MG orientation check, Tier 2 contact sheet, and Tier 3 contact sheet.
- Created zip package in Downloads.

The generator emits a Pillow deprecation warning for `Image.getdata`, but output generation succeeds and the warning does not affect this batch.

## Child QA

Read-only child QA approved the batch as visual-direction candidates over Hardpoint Pads V1, with cautions:

- Do not treat these as runtime-approved.
- Aid Shelter and Command Dugout are safer first acceptance targets than MG Nest or Mortar Emplacement.
- MG barrel must point north/up/front, with rear/operator access south/down/open.
- Mortar tube should be short, fat, and straight, not a curved rod.
- Foundation and under-construction states must remain incomplete.

Adjustments made:

- Under-construction structures were kept incomplete instead of active-with-toolbox.
- MG orientation check sheet was generated.
- MG barrel points north/up/front.
- Mortar tube was kept shorter/fatter than the MG barrel.

## Risks

- HardpointStructures V1 is visually generated but not gameplay-wired.
- MG and mortar structures remain orientation/manning/ammunition/targeting sensitive.
- Aid and command should be accepted first if the next gate is live runtime wiring.
- No Unity Play Mode or F9 visual validation was run in this pass.
- These are upgrade-tier candidates, not accepted runtime buildables.

## Cleanup

- No temporary scratch directories were left behind.
- Runtime output, review output, generator script, zip package, and this report were intentionally retained.
- The child QA agent was closed after completion.

## Follow-Up Recommendations

- Use Empty Hardpoint Pad first for claim/build flow.
- Then wire Aid Shelter or Command Dugout as the first role-specific hardpoint structure.
- Delay MG Nest and Mortar Emplacement function until emplacement-brain, manning, orientation, ammunition, targeting, and mission hooks are live.
- Decide later whether 8x8 hardpoints need their own distinct structure scale.
