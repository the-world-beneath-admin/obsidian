# TWB Trenchworks Rifle Fighting Positions Art Report

Date: 2026-05-22

## Scope

Standalone TWB-tagged Unity 2D game: TWB Trenchworks.

This pass created the next war-side art batch: tiered rifle fighting-position overlays for front-line trench sockets. It did not modify the raw GPT Pro package, permanent Obsidian wiki memory, or unrelated TWB projects.

## What Changed

- Created `RifleFightingPositions/V1` under the live Trenchworks Unity project.
- Generated 4 rifle-position families:
  - short rifle bay
  - long rifle bay
  - firestep pair
  - prone scrape pair
- Generated 3 visual tiers:
  - Tier 1 rough
  - Tier 2 reveted
  - Tier 3 reinforced
- Generated 4 orientations:
  - north
  - east
  - south
  - west
- Generated 7 visual states:
  - blueprint
  - foundation
  - under-construction
  - active-empty
  - active-occupied
  - damaged
  - destroyed
- Exported 336 transparent 192x192 PNGs.
- Exported a manifest with position family, tier, orientation, state, socket count, footprint hint, visual-only flag, normal/debug state flags, sort suggestion, and alpha metadata.
- Exported one active overview sheet and three per-tier contact sheets.
- Packaged the batch as `C:\Users\yrred\Downloads\twb-trenchworks-rifle-fighting-positions-v1.zip`.
- Updated the Trenchworks art catalog and active task brief.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_rifle_fighting_positions_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\SolidAssets\RifleFightingPositions\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\rifle-fighting-positions-v1\`
- `C:\Users\yrred\Downloads\twb-trenchworks-rifle-fighting-positions-v1.zip`

## Review Images

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\rifle-fighting-positions-v1\rifle-fighting-positions-v1-active-overview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\rifle-fighting-positions-v1\rifle-fighting-positions-v1-tier1-rough-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\rifle-fighting-positions-v1\rifle-fighting-positions-v1-tier2-reveted-contact-sheet.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\rifle-fighting-positions-v1\rifle-fighting-positions-v1-tier3-reinforced-contact-sheet.png`

## Child QA

Child reviewer Harvey (`019e52aa-6a95-7bf0-ab8f-265d4c43ef98`) audited the required coverage as a read-only execution child.

Key result:

- The pack needed short and long rifle bays, orientation variants, three tiers, clear empty socket handling, and occupied/debug variants kept separate from normal play.
- The pack must not duplicate MG sockets, MG nests, hardpoint pads, completed hardpoint structures, mortars, aid shelters, or command dugouts.
- The manifest should state socket count, footprint, sorting, walkability, and visual-only/debug flags. These fields are present in the generated manifest.

## Checks Run

- Generated rifle-position pack with:
  - `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_rifle_fighting_positions_v1.py`
- Mechanical sprite QA:
  - Rifle-position PNG count: 336 / expected 336.
  - Dimensions: 192x192.
  - Bad alpha/dimension sample count: 0.
- Zip QA:
  - Zip entries: 343.
  - Asset PNGs in zip: 336.
  - Review PNGs in zip: 4.
  - Manifest included: yes.
  - Generator included: yes.
- Visual review:
  - Opened active overview sheet.
  - Opened Tier 2 contact sheet.

## Cleanup Performed

- The generator removes stale `.png`, `.json`, and `.md` outputs in its dedicated output and review folders before regenerating.
- No source files were deleted outside the intended RifleFightingPositions V1 output/review folders.
- No raw GPT Pro package files were modified.
- Child worker was closed after review.
- Temporary heartbeat was deleted after the child review and packaging completed.

## Risks

- Unity/F9 runtime validation was not run.
- Sorting, socket preservation, scale, pivot, trench attachment, and rotation must be proven in Unity.
- Active-occupied variants are deliberately marked as debug/socket-validation states; normal runtime should use unit sprites for actual soldiers unless Bob chooses otherwise.
- Rifle positions are visual-only overlays in the manifest. They should not claim hardpoint ownership, ammunition, manning, or mission hooks.

## Memory-Worthy Notes

- `RifleFightingPositions/V1` closes the catalog's dedicated rifle fighting-position source pass at the art-candidate level.
- This pack is separate from MG sockets, hardpoint pads, and hardpoint structures.
- The next nearby art gap is likely front-line MG socket empty/debug overlays or support/service/rear trench-line visual language.

## Follow-Up Recommendations

- Runtime-test one tier and all four orientations over a trench line before exposing rifle positions in normal play.
- Keep active-occupied variants debug-only until the unit renderer can prove socket alignment.
- Generate front-line MG socket empty/debug overlays separately so rifle bays and MG nests stay visually distinct.
