# TWB Trenchworks Support Emplacement Solid Asset Pack Report

Date: 2026-05-22
Scope: TWB Trenchworks standalone Unity project

## What changed

Created a first-pass war-side solid asset pack for support emplacements:

- Mortar Pit
- Aid Post
- Command Dugout
- Supply Niche

Each asset has five gameplay states:

- Blueprint
- Under Construction
- Active
- Damaged
- Destroyed

The runtime assets are transparent 192x192 PNGs intended for Unity import and later wiring into construction/state logic. Review sheets were generated for quick visual inspection.

Update: Rebuilt the mortar pit after visual review. The active/under-construction/damaged mortar now uses a deliberately chunky straight tube with an open muzzle and base plate so it reads clearly at game zoom.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_support_emplacements_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\SolidAssets\SupportEmplacements\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\support-emplacements-v1\`

Generated runtime assets:

- `support-emplacement-v1-mortar-pit-*.png`
- `support-emplacement-v1-aid-post-*.png`
- `support-emplacement-v1-command-dugout-*.png`
- `support-emplacement-v1-supply-niche-*.png`
- `support-emplacements-v1-manifest.json`
- `README.md`

Generated review assets:

- `support-emplacements-v1-contact-sheet.png`
- `support-emplacements-v1-active-examples.png`

Packaged archive:

- `C:\Users\yrred\Downloads\twb-trenchworks-support-emplacements-v1.zip`

## Tests/checks run

- Ran the procedural generator successfully.
- Verified 20 runtime PNGs were generated.
- Verified every runtime PNG is 192x192.
- Verified every runtime PNG has non-empty alpha.
- Visually reviewed the active examples sheet.
- Visually reviewed the full contact sheet.

## Cleanup performed

- No temporary scratch images were left outside the intended runtime and review directories.
- Child worker attempt was closed after timeout and local generation completed inline.

## Risks

- These are first-pass procedural sprites, not final hand-painted production polish.
- The pack is not yet wired into Unity gameplay/build menus/state machines.
- Unity import settings and sprite pivots still need to be configured or generated through `.meta` files during integration.
- Pillow emitted a future deprecation warning for `Image.getdata`; this does not affect current output.

## Memory-worthy notes

- War-side "solid assets" now have a clearer pattern: transparent runtime PNGs, a manifest, a local README, and review/contact sheets.
- Support emplacements should remain gameplay/stateful assets, separate from decoration assets such as rubble piles, loose trash, rocks, foliage, and small scenery clutter.
- Initial guidance for this pack: pivot `[96,112]`, sort point `[96,130]`, intended footprint `3x3` cells.

## Follow-up recommendations

- Wire these four support emplacement kinds into the solid asset catalog and Unity spawn/build pipeline.
- Add Unity import settings or an importer pass for sprite pivot/sort consistency.
- After wiring, create the next solid-asset pack for larger battlefield structures such as bunker variants, artillery logistics, and command/signal upgrades.
