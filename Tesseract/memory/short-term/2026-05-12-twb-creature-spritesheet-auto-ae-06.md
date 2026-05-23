# TWB Creature Sprite Sheet Automation Report - AE-06

## Task

Automated creature sprite-sheet production worker run for the main game, The World Beneath.

Process exactly one family triad package from the Tier 1 creature walk sprite-sheet queue.

## Chunk Processed

- Chunk: AE-06
- Affinity: arcane-engineering
- Biome: marine
- Family: Tideclamp Crabs
- Creatures:
  - atk-clampclaw-crab
  - def-barnacle-bracket-snail
  - util-buoykey-plover

## Result

QA Passed.

All three AE-06 creature walk sheets were generated, finished, repacked, mechanically QA checked, visually inspected, and written beside their source card art. `CHUNK_QUEUE.md` was updated only after all three passed.

The first Buoykey Plover generation attempt was rejected because its direction rows were too side-view heavy and ambiguous. A second stricter prompt produced usable down, left, right, and up rows.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\atk-clampclaw-crab-creature-pet-t1-arcane-engineering-zeta-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\atk-clampclaw-crab-creature-pet-t1-arcane-engineering-zeta-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\atk-clampclaw-crab-creature-pet-t1-arcane-engineering-zeta-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\def-barnacle-bracket-snail-creature-pet-t1-arcane-engineering-zeta-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\def-barnacle-bracket-snail-creature-pet-t1-arcane-engineering-zeta-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\def-barnacle-bracket-snail-creature-pet-t1-arcane-engineering-zeta-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\util-buoykey-plover-creature-pet-t1-arcane-engineering-zeta-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\util-buoykey-plover-creature-pet-t1-arcane-engineering-zeta-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\marine\util-buoykey-plover-creature-pet-t1-arcane-engineering-zeta-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-creature-spritesheet-auto-ae-06.md`

## Generated Source Images

Raw generated-image provenance was left in place under `C:\Users\yrred\.codex\generated_images\`.

- Accepted Clampclaw Crab raw sheet: `C:\Users\yrred\.codex\generated_images\019e1aa5-cefd-76e2-9ece-11f02b215525\ig_0d82a244a326c73b016a02ba2fd1e08195b76c02a7d9a9176f.png`
- Accepted Barnacle Bracket Snail raw sheet: `C:\Users\yrred\.codex\generated_images\019e1aa5-cefd-76e2-9ece-11f02b215525\ig_0d82a244a326c73b016a02bade4c888195b12f9e82f11ab428.png`
- Rejected Buoykey Plover raw sheet: `C:\Users\yrred\.codex\generated_images\019e1aa5-cefd-76e2-9ece-11f02b215525\ig_0d82a244a326c73b016a02bc1c3b848195b9d8a4a4b75fe2fa.png`
- Accepted Buoykey Plover raw sheet: `C:\Users\yrred\.codex\generated_images\019e1aa5-cefd-76e2-9ece-11f02b215525\ig_0d82a244a326c73b016a02bd6ff4e08195bde45b91d64c459d.png`

Finished-alpha intermediate sheets remain under:

`C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\tmp\AE-06`

They were left because the manifests record them as the repack input provenance.

## Checks Run

For each final creature sheet:

- PNG exists beside source card art.
- PNG size is 1024x1024.
- PNG mode is RGBA.
- Alpha extrema include 0 and 255.
- All four corner alpha values are 0.
- All 16 cells have non-empty alpha content.
- `.png.meta` exists.
- `.png.meta` contains `spriteMode: 2`.
- `.png.meta` contains `alphaIsTransparency: 1`.
- `.png.meta` contains 16 unique slice names.
- `.manifest.json` exists and records row order as down, left, right, up.
- Final chroma edge sniff found 0 magenta and 0 lime/green edge-dust pixels after cleanup.

Minimum per-cell margins after final cleanup:

- Clampclaw Crab: left 13 px, top 48 px, right 13 px, bottom 12 px.
- Barnacle Bracket Snail: left 13 px, top 70 px, right 13 px, bottom 12 px.
- Buoykey Plover: left 13 px, top 24 px, right 13 px, bottom 12 px.

Visual inspection:

- Clampclaw Crab row order reads as down/front, left, right, up/back; no visible matte fringe.
- Barnacle Bracket Snail row order reads as down/front, left, right, up/back; no visible matte fringe.
- Buoykey Plover accepted second generation reads as down/front, left, right, up/back; no visible matte fringe.

## Finishing Pass Performed

- Used flat magenta `#FF00FF` matte only.
- Ran chroma removal with soft matte, edge contract, and despill.
- Repacked through `tools\art\repack_creature_walk_sheet.py`.
- Performed an additional final low-alpha chroma dust cleanup on the repacked PNGs:
  - Clampclaw Crab: 11 pixels cleaned.
  - Barnacle Bracket Snail: 114 pixels cleaned.
  - Buoykey Plover: 129 pixels cleaned.
- Reran QA after cleanup.

## Cleanup Performed

- No broad cleanup or revert operations were run.
- No source art, raw generated provenance, reports, or other worker files were deleted.
- Finished-alpha intermediate files were retained because the manifests reference them as repack input provenance.

## Blockers

None.

## Risks

- Mechanical QA does not prove in-engine animation feel. Unity/import or gameplay preview may still reveal motion quirks.
- Bird/plover walk cycles are visually usable, but the first attempt showed that plover direction rows need stricter prompting than quadrupeds or crawling creatures.
- Pixel-art outlines are intentionally preserved; the final chroma sniff only verifies no magenta/lime matte dust remains.

## Memory-Worthy Notes

- AE-06 / arcane-engineering / marine is complete and marked QA Passed.
- Stricter direction-row language helped correct the Buoykey Plover generation: explicitly say front/down, left-facing side, right-facing side, and back/up.
- A small final low-alpha chroma dust cleanup after repack is useful because antialiasing/resampling can leave alpha-1 key-color pixels even after the matte-removal pass.

## Do-Not-Promote Notes

- Do not promote rejected plover visual details as canon; that sheet was rejected for ambiguous direction rows.
- Do not promote raw generated file names except as provenance if needed.

## Follow-Up Recommendations

- Next automation run should process AE-07 / arcane-engineering / park only.
- Consider making the final low-alpha chroma dust cleanup a formal helper step before future QA.
