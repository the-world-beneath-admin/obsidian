# TWB Creature Sprite Sheet Automation - CU-04

- Task: TWB Sprite Sheet Single Runner.
- Run time: 2026-05-13T13:45:53.2326356-05:00.
- Automation ID: `twb-sprite-sheet-triad-runner`.
- Lock status: Acquired singleton lock at `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json`; intended chunk updated to `CU-04 / cunning / grassland`.
- Chunk processed: `CU-04` / `cunning` / `grassland`.
- Result: Complete. `CHUNK_QUEUE.md` updated to `QA Passed` after all three creatures passed generation, finishing, repack, mechanical QA, and visual QA.

## Creatures Completed

- `atk-barbspur-shrike`
  - Final PNG: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\atk-barbspur-shrike-creature-pet-t1-cunning-zeta-atk-walk-4dof-1024.png`
  - Meta: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\atk-barbspur-shrike-creature-pet-t1-cunning-zeta-atk-walk-4dof-1024.png.meta`
  - Manifest: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\atk-barbspur-shrike-creature-pet-t1-cunning-zeta-atk-walk-4dof-1024.manifest.json`
- `def-burrhide-badger`
  - Final PNG: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\def-burrhide-badger-creature-pet-t1-cunning-zeta-def-walk-4dof-1024.png`
  - Meta: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\def-burrhide-badger-creature-pet-t1-cunning-zeta-def-walk-4dof-1024.png.meta`
  - Manifest: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\def-burrhide-badger-creature-pet-t1-cunning-zeta-def-walk-4dof-1024.manifest.json`
- `util-whisperclick-katydid`
  - Final PNG: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\util-whisperclick-katydid-creature-pet-t1-cunning-zeta-util-walk-4dof-1024.png`
  - Meta: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\util-whisperclick-katydid-creature-pet-t1-cunning-zeta-util-walk-4dof-1024.png.meta`
  - Manifest: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\util-whisperclick-katydid-creature-pet-t1-cunning-zeta-util-walk-4dof-1024.manifest.json`

## Files Touched

- Updated queue: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- Wrote final creature assets beside source card art under `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\grassland\`.
- Retained accepted generated inputs under `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-04\` because manifests reference cleaned generated sheets.
- Raw generated provenance retained under `C:\Users\yrred\.codex\generated_images\019e2295-581d-7530-b167-7d80e43a3748\`.

## Checks Run

- Used source card art as identity lock for each creature.
- Generated full 4x4 walk sheets on flat magenta `#FF00FF` only.
- Rejected first katydid generation because the top row was too side-biased for `down/front`; regenerated the same creature once with stricter row-order prompting.
- Ran `remove_chroma_key.py` with `#FF00FF`, soft matte, despill, and edge contraction on accepted generated sheets.
- Ran `tools\art\repack_creature_walk_sheet.py` for each accepted creature.
- Ran final finishing pass to zero sub-threshold alpha specks and low-alpha magenta/green residue.
- Ran consolidated mechanical QA:
  - PNG size `1024x1024`: pass for all three.
  - Mode `RGBA`: pass for all three.
  - Alpha extrema include `0` and `255`: pass for all three.
  - Four corner alpha values `0`: pass for all three.
  - All 16 cells populated: pass for all three.
  - 2 px outer sheet edge alpha: `0` for all three.
  - Exact visible `#FF00FF` / key-green pixels: `0` for all three.
  - Low-alpha chroma pixels: `0` for all three.
  - `.png.meta` exists with `spriteMode: 2`, `alphaIsTransparency: 1`, and 16 slice names: pass for all three.
  - `.manifest.json` exists with row order `down`, `left`, `right`, `up`, 256 px cells, and 16 placements: pass for all three.
- Visual QA performed in image viewer for each final sheet; row order usable as down/left/right/up and no visible matte/outline artifacts found.

## Finishing Pass Performed

- Chroma/matte spill removal: yes.
- Cutout halo and 1-2 px edge artifact cleanup: yes.
- Close visual silhouette sniff test: yes.
- Noted pixels zeroed by final pass:
  - Shrike: `25409`
  - Badger: `19896`
  - Katydid: `32000`

## Cleanup Performed

- No throwaway logs, previews, or scratch files were created.
- Accepted raw/copy and alpha generated inputs were retained because they are provenance and/or manifest-linked sources.
- Rejected first katydid raw generation was left in Codex generated-image provenance and not copied into the Unity pipeline folder.
- Singleton lock is to be released after this report and automation memory are updated.

## Blockers

- None.

## Risks

- Mechanical QA cannot prove animation feel in-engine; it only confirms the asset contract and visible sheet sanity.
- Katydid required one regeneration for clearer direction rows. The accepted version is usable, but antenna-heavy insects remain a higher visual-risk category.

## Memory-Worthy Notes

- `CU-04` / `cunning` / `grassland` is complete and marked `QA Passed`.
- Completed this run: `atk-barbspur-shrike`, `def-burrhide-badger`, `util-whisperclick-katydid`.
- Next pending queue target is `CU-05` / `cunning` / `industrial`.

## Do-Not-Promote Notes

- Do not promote the first raw katydid generation as accepted; it was rejected for side-biased direction rows.
- Do not promote raw generated magenta sheets as final assets; only the repacked transparent RGBA outputs are final.

## Follow-Up Recommendations

- Next automation run should process exactly one package: `CU-05` / `cunning` / `industrial`.
