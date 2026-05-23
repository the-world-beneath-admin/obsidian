# TWB Trenchworks Battlefield Cover Solid Asset Pack Report

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity project

## What changed

Created a fifth war-side solid asset pack for cover-bearing battlefield structures:

- Shell-Crater Cover
- Ruined Wall Segment
- Collapsed Wagon Barricade
- Shallow Foxhole

Each asset has five gameplay states:

- Blueprint
- Under Construction
- Active
- Damaged
- Destroyed

The runtime assets are transparent 192x192 PNGs intended for Unity import and later wiring into cover, line-of-sight, suppression, or pathing logic. Review sheets were generated for quick visual inspection.

## Child-agent review

A bounded child worker reviewed the proposed batch and flagged the main risks: crater versus foxhole confusion, wagon overlap with barricade assets, wall overlap with rubble, and too much sandbag language making found cover feel like built emplacements. The generator was adjusted to reduce sandbags, strengthen the crater hollow, keep the foxhole lower and smaller, and make the wagon wheels clear.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_battlefield_cover_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\SolidAssets\BattlefieldCover\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\battlefield-cover-v1\`

Generated runtime assets:

- `battlefield-cover-v1-shell-crater-cover-*.png`
- `battlefield-cover-v1-ruined-wall-segment-*.png`
- `battlefield-cover-v1-collapsed-wagon-barricade-*.png`
- `battlefield-cover-v1-shallow-foxhole-*.png`
- `battlefield-cover-v1-manifest.json`
- `README.md`

Generated review assets:

- `battlefield-cover-v1-contact-sheet.png`
- `battlefield-cover-v1-active-examples.png`

Packaged archive:

- `C:\Users\yrred\Downloads\twb-trenchworks-battlefield-cover-v1.zip`

## Tests/checks run

- Ran the procedural generator successfully.
- Verified 20 runtime PNGs were generated.
- Verified every runtime PNG is 192x192.
- Verified every runtime PNG has non-empty alpha.
- Visually reviewed the active examples sheet.
- Visually reviewed the full contact sheet.

## Cleanup performed

- Cleared and regenerated the pack after incorporating the child QA feedback.
- Removed a misleading black-silhouette review sheet from the output because shared ground footprints made it read as four identical blobs rather than a useful review artifact.
- Closed the child QA worker after using its recommendation.
- Removed the 2-minute heartbeat after completion.

## Risks

- These are first-pass procedural sprites, not final hand-painted production polish.
- The pack is not yet wired into Unity gameplay/build menus/state machines.
- Crater and foxhole must remain visually distinct in live scale; the current pass improves this but should be checked in Unity.
- Unity import settings and sprite pivots still need to be configured or generated through `.meta` files during integration.
- Pillow emitted a future deprecation warning for `Image.getdata`; this does not affect current output.

## Memory-worthy notes

- Battlefield cover should be treated as a gameplay solid asset lane distinct from support emplacements, heavy structures, field obstacles, and sector infrastructure.
- This pack should be used as cover/readability proof, not as decoration rubble.
- Initial guidance for this pack: pivot `[96,116]`, sort point `[96,134]`, intended footprint `3x2` cells.

## Follow-up recommendations

- Wire this pack into the solid asset catalog and Unity build/spawn pipeline only after deciding how cover affects combat resolution.
- Add a live Unity visual check for crater versus foxhole readability at actual zoom levels.
- Avoid further rubble/cover batches until these four are tested against existing cover art and gameplay needs.
