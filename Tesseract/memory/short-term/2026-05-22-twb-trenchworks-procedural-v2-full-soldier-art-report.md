# TWB Trenchworks Procedural V2 Full Soldier Art Report - 2026-05-22

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

This pass was limited to generating a first complete new-system procedural soldier/unit art matrix for the current Trenchworks role/action shape. It did not modify old V2 unit art, other TWB projects, permanent Obsidian memory, Unity runtime code, or the raw GPT Pro package.

## Requirement Derived From Current State

Current runtime/catalog evidence shows:

- `PrototypeBootstrap.cs` expects `ExpectedWarMemberRoleCatalogCount = 33`.
- Runtime unit frame paths are currently built as individual frame PNGs under `Art/War/Units/V2/Cutouts/{Action}/{role}/{role}-{action}-{direction}-{frame}.png`.
- Current action folders are `Move`, `Crouch`, `Crawl`, `Primary`, and `Secondary`.
- Each populated V2 action folder has 33 role directories and 528 PNGs, meaning 33 roles x 4 directions x 4 frames.

This pass therefore targeted:

- 33 roles
- 5 actions
- 4 directions: `down`, `left`, `right`, `up`
- 4 frames per direction
- 165 role/action sheets
- 2,640 individual frame PNGs under Art
- 2,640 individual frame PNGs under Resources

## Summary

Generated first-pass procedural art coverage for all 33 current soldier/unit roles across the current five runtime actions:

- `Move`
- `Crouch`
- `Crawl`
- `Primary`
- `Secondary`

The art is intentionally category-based procedural coverage rather than bespoke final illustration per role. The goal of this pass was complete matrix coverage with readable posture and role cues under the new deterministic system.

## Work Completed

- Created the full-matrix procedural generator:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v2_full_soldier_units.py`
- Created the local full-matrix unit-art contract:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\procedural_v2_full_unit_art_contract.md`
- Created the frame export/QA repair helper:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\export_procedural_v2_full_frames_and_qa.py`
- Generated per-role/action transparent runtime sheets, cyan source sheets, manifests, QA JSON, Resources mirrors, and individual frame exports.
- Generated action overview PNGs and a showcase overview.

## Key Output Paths

Review root:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full
```

Main summaries:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-summary.json
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-frame-export-summary.json
```

Overview images:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-showcase-overview.png
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-overview-move.png
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-overview-crouch.png
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-overview-crawl.png
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-overview-primary.png
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\Review\procedural-v2-full\procedural-v2-full-overview-secondary.png
```

Generated art roots:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV2Full
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Resources\Art\War\Units\ProceduralV2Full
```

Individual frame roots:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\ProceduralV2Full\Cutouts
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Resources\Art\War\Units\ProceduralV2Full\Cutouts
```

## Counts Verified

- 33 roles.
- 5 actions.
- 165 role/action pairs.
- 165 transparent 256 x 256 RGBA sheets.
- 165 cyan source sheets.
- 165 manifests.
- 165 per-role/action QA JSON files.
- 2,640 Art frame PNGs.
- 2,640 Resources frame PNGs.
- 6 review PNGs.

## Checks Run

- `python -m py_compile C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v2_full_soldier_units.py` - passed.
- `python -m py_compile C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\export_procedural_v2_full_frames_and_qa.py` - passed.
- `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\generate_procedural_v2_full_soldier_units.py --validate-only` - passed with `all_valid: true`.
- `python C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unit-art-generation\export_procedural_v2_full_frames_and_qa.py --validate-only` - passed with `all_valid: true`.
- Parent physical count check confirmed:
  - 2,640 Art frame PNGs.
  - 2,640 Resources frame PNGs.
  - 165 QA JSON files.
- Parent sample frame checks confirmed 64 x 64 RGBA frames for:
  - stretcher-bearer secondary frame.
  - MG gunner primary frame.
- Rendered showcase, crawl, and secondary overview images in Codex image view.
- Verified raw GPT Pro catalog hash remained unchanged:
  - `EB3701497C8B7E1A0F82BA50D09F795A198B52AC9C4FED65E8C5B824D0DDBF55`
- Unity import, sprite slicing, live runtime mapping, Play Mode, and F9 checks were not run.

## Source Policy

- No old V2 soldier PNGs, screenshots, cutouts, sheets, or frames were used as visual inputs.
- No old ProceduralV1 outputs were used as visual inputs.
- No image generation was used.
- The generated frame exports use only the current ProceduralV2Full transparent sheets as inputs.
- The raw Obsidian/GPT Pro package was not modified.

## Current State

The first complete new-system soldier/unit art matrix now exists for the current runtime role/action shape. It includes movement, crouch, crawl, primary/rifle or tool position, and secondary/support posture coverage.

Specialist cues included in the first-pass procedural system include rifle, engineer tools, medical bags/crosses, stretcher/carry cue, MG tripod, marksman long rifle/scope, wire tools/spool, signal flag/aerial, mortar tube, logistics crates/packs, command maps/markers, and occult/support variants.

## Risks / Fragile Areas

- This is first-pass procedural coverage, not final bespoke art polish.
- Some role distinctions are category-level and will need art-direction review before promotion.
- Current runtime code still points to old `V2\Cutouts` paths. A separate integration pass is required to map runtime loading to `ProceduralV2Full` paths or to create an approved migration plan.
- Unity import settings, pivots, sprite slicing, animation playback, scale, sorting, and in-scene readability remain unverified.

## Memory-Worthy Notes

- Fact: ProceduralV2Full now covers all 33 current unit roles across `Move`, `Crouch`, `Crawl`, `Primary`, and `Secondary`.
- Fact: The generated matrix contains 165 role/action sheets and 2,640 individual frame PNGs under both Art and Resources cutout roots.
- Fact: The main review root is `Assets\Art\War\Units\Review\procedural-v2-full`.
- Fact: The helper scripts are `generate_procedural_v2_full_soldier_units.py` and `export_procedural_v2_full_frames_and_qa.py`.
- Warning: The art is not yet Unity/F9 accepted and runtime mapping still points at V2 paths.

## Do Not Promote

- Do not promote these as final runtime soldier art until Unity import/runtime mapping and F9 visual validation pass.
- Do not treat old V2 unit art as source input for this new procedural system.
- Do not overwrite the existing V2 cutouts until an explicit migration gate approves it.

## Cleanup Performed

- Deleted the full-soldier-art heartbeat automation after child work completed.
- Closed both child subagents after reviewing their results.
- Child cleanup removed compile `__pycache__` artifacts.
- No broad cleanup was performed.

## Next Recommended Gate

Run a narrow Unity integration review for one action and a small role subset first, ideally `rifleman`, `stretcher_bearer`, `mg_gunner`, and `field_engineer`. Confirm Resources loading, sprite pivots, animation frame timing, scale, and in-scene readability before migrating all runtime role mappings away from V2.
