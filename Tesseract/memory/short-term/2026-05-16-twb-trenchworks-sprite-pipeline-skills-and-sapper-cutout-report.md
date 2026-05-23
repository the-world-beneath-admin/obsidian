# TWB Trenchworks Sprite Pipeline Skills And Sapper Cutout Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D, reusable TWB game-asset sprite pipeline.

## What Changed

- Created reusable Codex skill `game-sprite-sheet-generator`.
  - Purpose: standardize sprite-sheet generation prompts around flat chroma-key backgrounds, black outlines, regular grids, direction rows, padding, and review-before-cutout rules.
- Created reusable Codex skill `cyan-sprite-sheet-cleaner`.
  - Purpose: standardize approved-sheet cleanup with the three-sweep cyan process, frame cutting, previews, and QA notes.
- Added deterministic cleaner script:
  - `C:\Users\yrred\.codex\skills\cyan-sprite-sheet-cleaner\scripts\clean_cyan_sprite_sheet.py`
- Approved Sapper was promoted to accepted source and processed through the new cleaner skill.
- Sapper now has five transparent sheets and `80` cut `128 x 128` frames.
- Updated the Trenchworks v2 unit-sheet index.

## Files Touched

- `C:\Users\yrred\.codex\skills\game-sprite-sheet-generator\SKILL.md`
- `C:\Users\yrred\.codex\skills\game-sprite-sheet-generator\references\prompt-templates.md`
- `C:\Users\yrred\.codex\skills\cyan-sprite-sheet-cleaner\SKILL.md`
- `C:\Users\yrred\.codex\skills\cyan-sprite-sheet-cleaner\references\three-sweep-cleanup.md`
- `C:\Users\yrred\.codex\skills\cyan-sprite-sheet-cleaner\scripts\clean_cyan_sprite_sheet.py`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sheets-v2-index.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sapper-v2-cutout-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sapper-v2-transparent-cutout-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sapper-v2-*-cutout-qa.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\war-unit-sapper-v2-*-cutout-preview.png`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Accepted\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Sheets\Transparent\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Art\War\Units\V2\Cutouts\`

## Tests And Checks Run

- Ran `quick_validate.py` on both new skills; both passed.
- Ran `py_compile` on the cleaner script; passed.
- Ran cleaner script on all five Sapper approved source sheets.
- Verified Sapper frame count: `80`.
- Verified Sapper transparent sheets have corner alpha `[0, 0, 0, 0]`.
- Verified Sapper combined QA found `0` remaining cyan-family opaque pixels in each transparent sheet.
- Installed `PyYAML` with `python -m pip install --user PyYAML` because the official skill validator required it and the local Python environment did not have it.

## Cleanup Performed

- No scratch files were left in the Trenchworks project tree.
- Original generated source images were preserved; accepted project copies remain under the asset tree.

## Risks

- The new skills are available for future Codex sessions, but they may require a new session/tool context refresh before appearing in the automatic skill list.
- The cleaner script currently expects PNG-like raster sheets and regular grids. Irregular atlases or hand-packed sheets should not use it without extension.
- `cell` fit mode is correct for square standard unit sheets; command/tall units should use `bbox` fit mode.

## Memory-Worthy Notes

- Repeated sprite-sheet generation/cleanup is now promoted from chat ritual into reusable Codex skills.
- The cyan cleanup standard is now formalized: exterior cyan, cyan-family fringe, interior cyan, plus final post-resize cyan catch.
- Sapper is complete. Troop progress is now `4 / 24`; `20 / 24` remain.
- Next queued unit is `war-unit-combat-medic-v2`, but it was not generated during this pass because the user requested pipeline solidification first.

## Follow-Up Recommendations

- Use `game-sprite-sheet-generator` before generating the next unit.
- Use `cyan-sprite-sheet-cleaner` after the next unit is approved.
- Continue with Combat Medic once the user confirms the new pipeline direction is acceptable.

## Anything Blocked

- No blocker for the new skills or Sapper cutout.
- Next unit generation is intentionally paused until user confirms moving forward after this pipeline pass.
