# TWB Creature Sprite Sheet Automation - CU-05

- Task: TWB Sprite Sheet Single Runner.
- Run time: 2026-05-13T15:01:49.434359-05:00.
- Automation ID: `twb-sprite-sheet-triad-runner`.
- Lock status: Acquired singleton lock at `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json`; intended chunk updated to `CU-05 / cunning / industrial`; released after report and memory update.
- Chunk processed: `CU-05` / `cunning` / `industrial`.
- Result: Complete. `CHUNK_QUEUE.md` updated to `QA Passed` after all three creatures passed generation, finishing, repack, mechanical QA, and visual QA.

## Creatures Completed

- `atk-rivetwink-ferret`
  - Final PNG: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\atk-rivetwink-ferret-creature-pet-t1-cunning-slot10-atk-walk-4dof-1024.png`
  - Meta: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\atk-rivetwink-ferret-creature-pet-t1-cunning-slot10-atk-walk-4dof-1024.png.meta`
  - Manifest: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\atk-rivetwink-ferret-creature-pet-t1-cunning-slot10-atk-walk-4dof-1024.manifest.json`
- `def-soottag-grub`
  - Final PNG: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\def-soottag-grub-creature-pet-t1-cunning-slot10-def-walk-4dof-1024.png`
  - Meta: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\def-soottag-grub-creature-pet-t1-cunning-slot10-def-walk-4dof-1024.png.meta`
  - Manifest: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\def-soottag-grub-creature-pet-t1-cunning-slot10-def-walk-4dof-1024.manifest.json`
- `util-ventlace-moth`
  - Final PNG: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\util-ventlace-moth-creature-pet-t1-cunning-slot10-util-walk-4dof-1024.png`
  - Meta: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\util-ventlace-moth-creature-pet-t1-cunning-slot10-util-walk-4dof-1024.png.meta`
  - Manifest: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\util-ventlace-moth-creature-pet-t1-cunning-slot10-util-walk-4dof-1024.manifest.json`

## Files Touched

- Updated queue: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- Wrote final creature assets beside source card art under `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\industrial\`.
- Retained accepted generated inputs under `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-05\` because manifests reference cleaned generated sheets.
- Raw generated provenance retained under `C:\Users\yrred\.codex\generated_images\019e22cc-bf30-78e2-8a12-58b6941ee692\`.

## Checks Run

- Used source card art as identity lock for each creature.
- Generated full 4x4 walk or hover-equivalent sheets on magenta-only matte prompts.
- Rejected two early Rivetwink generations: one for matte quality concern and one for insect-like antenna identity drift.
- Ran connected magenta matte removal, internal key-pocket cleanup where needed, edge decontamination, and 1-2 px fringe cleanup.
- Ran `tools\art\repack_creature_walk_sheet.py` for each accepted creature.
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
- Visual QA performed in image viewer for each final sheet; row order usable as down/left/right/up and no visible matte/outline artifacts found after finishing.

## Finishing Pass Performed

- Chroma/matte spill removal: yes.
- Cutout halo and 1-2 px edge artifact cleanup: yes.
- Close visual silhouette sniff test: yes.
- Noted finishing cleanup totals:
  - Rivetwink Ferret: connected matte `1115652`, source fringe `3400`, final zero/recolor passes applied.
  - Soottag Grub: connected matte `1001722`, source fringe `4052`, final zero/recolor passes applied.
  - Ventlace Moth: connected matte `1048454`, source fringe `8525`, internal magenta pockets removed before acceptance.

## Cleanup Performed

- Deleted temporary preview `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-05\atk-rivetwink-ferret-contract-preview.png`.
- No scratch scripts or throwaway logs were left.
- Accepted raw/copy and alpha generated inputs were retained because they are provenance and/or manifest-linked sources.
- Singleton lock released after this report and automation memory were updated.

## Blockers

- None.

## Risks

- Mechanical QA cannot prove animation feel in-engine; it confirms the asset contract and sheet sanity.
- The image generator still tends to render magenta backgrounds with slight gradients; final assets passed transparent-output QA after cleanup, but future runs should keep strict matte and identity prompts.
- Winged/antenna-heavy creatures remain high risk for enclosed key-color pockets; Ventlace required internal matte cleanup.

## Memory-Worthy Notes

- `CU-05` / `cunning` / `industrial` is complete and marked `QA Passed`.
- Completed this run: `atk-rivetwink-ferret`, `def-soottag-grub`, `util-ventlace-moth`.
- Next pending queue target is `CU-06` / `cunning` / `marine`.

## Do-Not-Promote Notes

- Do not promote the first two raw Rivetwink generations as accepted; one had matte quality concerns and one introduced insect-like antenna identity drift.
- Do not promote raw generated magenta sheets as final assets; only the repacked transparent RGBA outputs are final.

## Follow-Up Recommendations

- Next automation run should process exactly one package: `CU-06` / `cunning` / `marine`.
