# TWB Trenchworks Worker Report - 2026-05-23

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

## Summary

Created `CommandAndMapMarkers/V1`, a war-side command/readability marker pack for command auras, order pips, status markers, emplacement state markers, war-map markers, minimap pips, and route-state mask pieces.

## Work Completed

- Generated `4,278` transparent PNG candidates under `Assets/Art/War/UI/CommandAndMapMarkers/V1`.
- Added world-space command overlays:
  - `128x128` command aura, command anchor, cohesion, and dispatch markers.
  - `64x64` order, status, mission, and emplacement markers.
- Added `64x64` war-map markers and `24x24` minimap pips for units, trenches, hardpoints, emplacements, contacts, objectives, front pressure, quiet-front recovery, and bombardment readiness.
- Added route-state mask pieces:
  - `64x64` war-map route masks.
  - `32x32` minimap route masks.
  - 16 NESW route masks for supply, spawn, blocked, and comms route families.
- Included friendly, enemy, and neutral faction palettes.
- Included normal/selected/urgent/stale states for map markers and open/supplied/strained/unsupplied/blocked/cut/debug-planned states for routes.
- Wrote manifest metadata marking these as not soldier sprites, not combat VFX, not decoration props, and not final HUD chrome.
- Spawned child QA/explorer `Linnaeus` for read-only contract review and incorporated its guidance around sizes, route masks, debug-only handling, and avoiding HUD-button confusion.
- Updated the Trenchworks art catalog and active brief.
- Packaged the results into `C:\Users\yrred\Downloads\twb-trenchworks-command-and-map-markers-v1.zip`.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\trench-art-generation\generate_command_and_map_markers_v1.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\art-pipeline\10_asset_catalog_twb_trenchworks.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\UI\CommandAndMapMarkers\V1\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Review\command-and-map-markers-v1\`
- `C:\Users\yrred\Downloads\twb-trenchworks-command-and-map-markers-v1.zip`

## Checks Run

- `python -m py_compile generate_command_and_map_markers_v1.py` passed.
- Generator completed with `4,278` PNGs.
- Mechanical PNG QA passed: `4,278` PNGs, `0` bad files, intended canvases only, visible alpha, no cyan or magenta chroma-key residue.
- Manifest/zip QA passed: `4,278` manifest entries, `4,278` asset PNGs in zip, `6` review PNGs in zip, manifest included, generator included.

Unity Play Mode/F9 validation was not run.

## Current State

`CommandAndMapMarkers/V1` is a complete first-pass command/map marker candidate set. It should be treated as art-pipeline ready, not runtime accepted.

## Risks / Fragile Areas

- These must not become bottom-button HUD chrome.
- These must not duplicate soldier status sprites or combat burst VFX.
- Debug hidden-plan markers must stay debug-only and never leak into normal play.
- Minimap markers still need live scale/readability proof.
- Route pieces still need renderer proof for NESW connection mapping.

## Memory-Worthy Notes

- Command/readability art needs separate sizing: large soft command auras, compact world order/status markers, tiny minimap pips, and NESW route mask pieces.
- Debug-hidden-plan art exists only as a developer overlay candidate.
- Final HUD panel chrome and factory UI icon art remain separate future surfaces.

## Do Not Promote

- Do not promote this pack as Unity/F9 accepted.
- Do not promote debug-only hidden plan art as player-facing.
- Do not treat this pack as proof that command/order/fog/minimap runtime behaviour is wired.

## Cleanup Performed

The generator cleans and recreates only its own output/review folders before generation. No raw GPT Pro package files were touched. The child heartbeat was used during QA and should be removed after final review.
