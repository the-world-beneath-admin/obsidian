# TWB Creature Spritesheet Auto - CU-07

- task: TWB Sprite Sheet Single Runner processed one family triad package.
- run time: 2026-05-13T16:43:13.7369803-05:00
- lock status: acquired with exclusive create semantics, updated with intended chunk `CU-07`, and held through report writing.
- chunk processed: `CU-07` / `cunning` / `park`.
- result: complete; all three creatures passed generation, repack, finishing pass, mechanical QA, and visual QA.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\atk-clipjaw-gremlin-creature-pet-t1-cunning-slot11-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\atk-clipjaw-gremlin-creature-pet-t1-cunning-slot11-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\atk-clipjaw-gremlin-creature-pet-t1-cunning-slot11-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\def-brakelatch-gremlin-creature-pet-t1-cunning-slot11-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\def-brakelatch-gremlin-creature-pet-t1-cunning-slot11-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\def-brakelatch-gremlin-creature-pet-t1-cunning-slot11-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\util-pathtag-gremlin-creature-pet-t1-cunning-slot11-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\util-pathtag-gremlin-creature-pet-t1-cunning-slot11-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\park\util-pathtag-gremlin-creature-pet-t1-cunning-slot11-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-07\atk-clipjaw-gremlin-creature-pet-t1-cunning-slot11-atk-generated-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-07\def-brakelatch-gremlin-creature-pet-t1-cunning-slot11-def-generated-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-07\util-pathtag-gremlin-creature-pet-t1-cunning-slot11-util-generated-cleaned.png`
- raw generated provenance retained under `C:\Users\yrred\.codex\generated_images\019e233c-221a-76d2-9cf2-293cf045830a\`.

## Checks Run

- Read required Tesseract and Unity sprite-sheet docs before production.
- Confirmed source card art in `affinities\cunning\park` and used it as identity reference.
- Generated one 4x4 sheet per creature using flat magenta `#FF00FF` matte only.
- Ran chroma removal with `remove_chroma_key.py` using `#FF00FF`, soft matte, edge contract, and despill.
- Ran `tools\art\repack_creature_walk_sheet.py` for each creature.
- Ran per-creature finishing pass: removed residual chroma-key pixels and normalized transparent RGB.
- Ran consolidated QA: all PNGs are `1024x1024` RGBA, alpha extrema include `0` and `255`, corner alpha values are `0`, all 16 cells populated, `.png.meta` exists, `spriteMode: 2`, `alphaIsTransparency: 1`, 16 slice names, `.manifest.json` exists, and visible key-color pixel checks passed.
- Visual QA: inspected final sheets at close zoom; row order reads as down / left / right / up and no visible matte, chroma fringe, or cutout halo artifacts were accepted.

## Finishing Pass Performed

- Attack sheet: removed 160 residual chroma pixels.
- Defence sheet: removed 104 residual chroma pixels.
- Utility sheet: removed 152 residual chroma pixels.
- No lime/green/magenta matte fringe remained after final QA; natural foliage colors were visually checked as subject detail rather than matte spill.

## Cleanup Performed

- No throwaway scripts, preview files, or logs were created.
- Cleaned generated inputs were retained because manifests reference them.
- Raw generated image provenance was retained under `.codex\generated_images` per pipeline practice.

## Blockers

- None.

## Risks

- Unity import/playback was not run in the editor; this run verified the PNG/meta/manifest contract and visual row usability only.
- As with prior automation runs, mechanical QA does not prove final animation feel in-game.

## Memory-Worthy Notes

- `CU-07` / `cunning` / `park` is complete and marked `QA Passed` in `CHUNK_QUEUE.md`.
- Completed creatures: `atk-clipjaw-gremlin`, `def-brakelatch-gremlin`, and `util-pathtag-gremlin`.
- Next pending queue target is `CU-08` / `cunning` / `rural_agricultural`.

## Do-Not-Promote Notes

- Do not promote raw per-pixel QA details unless debugging a future matte issue.
- Do not treat this report as Unity runtime validation.

## Follow-Up Recommendations

- Next automation run should process only `CU-08` if the singleton lock is free.
- Optional later pass: Unity import/playback spot-check for the completed cunning park triad.
