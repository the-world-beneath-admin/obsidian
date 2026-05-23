# TWB Creature Sprite Sheet Automation - AE-09 Complete

Run time: 2026-05-12T05:59:55-05:00
Automation ID: `twb-sprite-sheet-triad-runner`

## Task

Process exactly one pending family triad package for **Main game / The World Beneath** creature walk sprite sheets.

Selected chunk: `AE-09` / `arcane-engineering` / `temperate_forest`

Creatures:

- `atk-rulerbite-squirrel`
- `def-stakeback-badger`
- `util-plumbline-wren`

## Lock Status

- Singleton lock acquired with exclusive create-new semantics before queue selection.
- Lock updated after selection with intended chunk `AE-09`.
- No fresh competing lock was present.

## Result

`AE-09` completed and `CHUNK_QUEUE.md` updated to `QA Passed`.

Final assets were generated beside the source card art:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\temperate_forest\atk-rulerbite-squirrel-creature-pet-t1-arcane-engineering-eta-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\temperate_forest\def-stakeback-badger-creature-pet-t1-arcane-engineering-eta-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\temperate_forest\util-plumbline-wren-creature-pet-t1-arcane-engineering-eta-util-walk-4dof-1024.png`

Each has a sibling `.png.meta` and `.manifest.json`.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AE-09-alpha-sources\`
- Final PNG, `.png.meta`, and `.manifest.json` files for all three AE-09 creatures.

## Checks Run

- Generated one creature at a time using source card art as the identity lock.
- Repacked each accepted generated sheet with `tools\art\repack_creature_walk_sheet.py`.
- Mechanical QA confirmed for all three final sheets:
  - `1024x1024`
  - `RGBA`
  - alpha extrema include `0` and `255`
  - all corner alpha values are `0`
  - all `16` cells populated
  - `.png.meta` exists
  - `spriteMode: 2`
  - `alphaIsTransparency: 1`
  - `16` slice names
  - `.manifest.json` exists and loads
  - manifest generated-source sheet exists
- Visual QA confirmed usable row order as down/front, left, right, up/back.

## Finishing Pass Performed

- Used flat magenta `#FF00FF` as the temporary chroma matte.
- Removed chroma matte with the imagegen chroma-key helper.
- Rejected the first `util-plumbline-wren` generation because the top row read as side-facing instead of front/down.
- Rejected an overly aggressive decontamination pass because it introduced visible green edge artifacts.
- Repacked from corrected `*-alpha-bleed.png` sources after a safer alpha edge-bleed finish.
- Final visual sniff shows no visible magenta, green/lime, checkerboard, or matte outline artifacts.

## Cleanup Performed

- Removed failed `*-alpha-finished.png` artifacts created by the rejected over-decontamination pass.
- Preserved generated-image provenance under `C:\Users\yrred\.codex\generated_images\019e1bbf-6645-7853-bb3d-646d967c34ad\`.
- Preserved accepted alpha-source and alpha-bleed inputs under `AE-09-alpha-sources` because final manifests reference the accepted bleed inputs.

## Blockers

None.

## Risks

- Mechanical QA does not prove animation quality in-engine; Unity import/motion preview was not run.
- Rulerbite and Stakeback identity is game-ready but simplified from the larger card portrait, as expected for sprite-sheet scale.

## Memory-Worthy Notes

- `AE-09` / `arcane-engineering` / `temperate_forest` is now complete and queue-marked `QA Passed`.
- For bird sprites, explicitly requiring the top row to be front/down rather than side-facing materially improved row-order quality.
- Over-aggressive chroma decontamination can create green edge artifacts; use the safer chroma-key helper plus alpha edge-bleed approach instead.

## Do-Not-Promote Notes

- Do not promote the rejected first Wren generation as an accepted asset.
- Do not promote the failed over-decontamination pass; it was removed.

## Follow-Up Recommendations

- Next automation run should start at `AE-10` / `arcane-engineering` / `tropical_forest`.
- Consider adding the safe alpha edge-bleed finish as a reusable helper if this pattern continues to be useful.
