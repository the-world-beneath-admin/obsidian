# TWB Trenchworks Procedural V1 Soldier Art Report - 2026-05-22

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

This pass was limited to a fresh procedural soldier/unit source and review sample set. It did not touch other TWB projects, permanent Obsidian memory, old V2 unit art, or the raw GPT Pro package.

## Summary

Generated a fresh deterministic procedural sample set for three unit roles:

- `rifleman`
- `field_engineer`
- `combat_medic`

Each role has a 256 x 256 transparent runtime sheet containing 16 fixed-canvas frames. Frame contract is 64 x 64 px, 4 columns x 4 rows, with rows `down`, `left`, `right`, `up` and columns `idle`, `walk_1`, `walk_2`, `primary_tool_pose`.

## Work Completed

- Created the procedural unit-art helper:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v1_soldier_units.py`
- Created the local unit-art contract:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\procedural_v1_unit_art_contract.md`
- Created a QA summary:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\procedural_v1_unit_art_qa_summary.json`
- Generated transparent runtime sheets, cyan source sheets, manifests, and QA JSON for all three roles.
- Mirrored transparent runtime sheets under `Assets\Resources`.
- Generated per-role review contact sheets and one combined overview:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v1\procedural-v1-unit-overview.png`

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v1_soldier_units.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\procedural_v1_unit_art_contract.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\procedural_v1_unit_art_qa_summary.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\rifleman\war-unit-rifleman-procedural-v1-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\rifleman\war-unit-rifleman-procedural-v1-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\rifleman\war-unit-rifleman-procedural-v1-manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\rifleman\war-unit-rifleman-procedural-v1-qa.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\field_engineer\war-unit-field_engineer-procedural-v1-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\field_engineer\war-unit-field_engineer-procedural-v1-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\field_engineer\war-unit-field_engineer-procedural-v1-manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\field_engineer\war-unit-field_engineer-procedural-v1-qa.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\combat_medic\war-unit-combat_medic-procedural-v1-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\combat_medic\war-unit-combat_medic-procedural-v1-source-cyan.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\combat_medic\war-unit-combat_medic-procedural-v1-manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\combat_medic\war-unit-combat_medic-procedural-v1-qa.json`
- Matching transparent runtime-sheet mirrors under `Assets\Resources\Art\War\Units\ProceduralV1\{role}\`.
- Review sheets under `Assets\Art\War\Units\Review\procedural-v1\`.
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-twb-trenchworks-procedural-v1-soldier-art-report.md`

## Checks Run

- Child command: `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v1_soldier_units.py` - passed.
- `python -m py_compile C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v1_soldier_units.py` - passed.
- `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v1_soldier_units.py --validate-only` - passed:
  - `VALIDATION PASSED: 3 roles, 16 frames each, 256x256 sheets`
- Verified all six generated transparent runtime sheets are `256 x 256` RGBA:
  - three under `Assets\Art\War\Units\ProceduralV1`
  - three under `Assets\Resources\Art\War\Units\ProceduralV1`
- Verified each per-role QA JSON reports:
  - `pass: true`
  - 16 frames
  - 64 x 64 frame size
  - no issues
  - source policy passed
- Searched the helper for old visual input path patterns. It does not open old V2/unit art. Its `Image.open` usage is limited to validating the newly generated transparent outputs.
- Verified the raw GPT Pro catalog hash remained unchanged:
  - `EB3701497C8B7E1A0F82BA50D09F795A198B52AC9C4FED65E8C5B824D0DDBF55`
- Rendered the combined overview in Codex image view.
- Unity import, animation playback, pivot, and F9 live scene checks were not run.

## Current State

Bob can inspect the combined soldier overview here:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v1\procedural-v1-unit-overview.png
```

The individual runtime sheets are:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\rifleman\war-unit-rifleman-procedural-v1-transparent.png
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\field_engineer\war-unit-field_engineer-procedural-v1-transparent.png
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV1\combat_medic\war-unit-combat_medic-procedural-v1-transparent.png
```

The generated assets are fresh procedural candidate unit art, not yet Unity/F9-accepted runtime art.

## Risks / Fragile Areas

- These are source/review candidates. Unity import settings, pivots, sprite slicing, animation timing, and live in-scene readability remain unverified.
- Role silhouettes are intentionally simple for a first procedural slice. They may need art-direction polish before promotion beyond candidate status.
- Existing runtime unit callers may still point at V2 or older unit sheets until a separate integration pass maps the new paths.

## Memory-Worthy Notes

- Fact: Fresh procedural soldier candidate sheets now exist for `rifleman`, `field_engineer`, and `combat_medic`.
- Fact: The combined review image is `Assets\Art\War\Units\Review\procedural-v1\procedural-v1-unit-overview.png`.
- Fact: The helper script is `docs\unit-art-generation\generate_procedural_v1_soldier_units.py`.
- Fact: The manifests and QA JSON record that old soldier/unit visual assets were not used and image generation was not used.
- Warning: These are not Unity/F9 validated runtime assets yet.

## Do Not Promote

- Do not promote these as final runtime unit art until Unity import, pivot/slicing, animation playback, and in-scene readability validation pass.
- Do not treat old V2 unit PNGs, source sheets, transparent sheets, screenshots, cutouts, or generated frames as inputs for this fresh procedural set.

## Cleanup Performed

- Deleted the temporary soldier-art heartbeat automation after child completion.
- Closed the child subagent after reviewing its result.
- Deleted the `__pycache__` artifact created by the parent py_compile check.
- No broad cleanup was performed.

## Next Recommended Gate

Review the combined overview with Bob. If the direction is acceptable, run a narrow Unity import/slicing pass for `rifleman` first, then verify pivots, row/action playback, and in-scene scale before promoting the other roles.
