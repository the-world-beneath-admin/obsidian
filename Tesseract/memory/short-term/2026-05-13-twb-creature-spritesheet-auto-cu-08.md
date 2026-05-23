# TWB Creature Sprite Sheet Automation - CU-08

- Task: Automated TWB creature sprite-sheet single triad production worker.
- Run time: 2026-05-13T17:49:14.5289332-05:00.
- Lock status: Singleton lock acquired normally before queue selection at `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json`; intended chunk updated to `CU-08`; lock released after report, memory update, and cleanup.
- Chunk processed: `CU-08` / `cunning` / `rural_agricultural`.
- Result: Completed and marked `QA Passed` in `CHUNK_QUEUE.md`.

## Creatures Completed

- `atk-stubblepicker-stitchling`
- `def-sackhide-stitchling`
- `util-rowghost-stitchling`

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\atk-stubblepicker-stitchling-creature-pet-t1-cunning-slot12-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\atk-stubblepicker-stitchling-creature-pet-t1-cunning-slot12-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\atk-stubblepicker-stitchling-creature-pet-t1-cunning-slot12-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\def-sackhide-stitchling-creature-pet-t1-cunning-slot12-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\def-sackhide-stitchling-creature-pet-t1-cunning-slot12-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\def-sackhide-stitchling-creature-pet-t1-cunning-slot12-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\util-rowghost-stitchling-creature-pet-t1-cunning-slot12-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\util-rowghost-stitchling-creature-pet-t1-cunning-slot12-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\rural_agricultural\util-rowghost-stitchling-creature-pet-t1-cunning-slot12-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-08\atk-stubblepicker-stitchling-walk-generated-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-08\def-sackhide-stitchling-walk-generated-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-08\util-rowghost-stitchling-walk-generated-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`

## Checks Run

- Read required Tesseract memory lane files and Unity art-pipeline docs before production.
- Used the source card art as the identity lock for each creature.
- Generated one 4x4 sprite sheet per creature using flat magenta `#FF00FF` matte only.
- Ran `remove_chroma_key.py` with magenta key, soft matte, despill, and edge contraction.
- Ran `tools\art\repack_creature_walk_sheet.py` for each creature.
- Ran individual and consolidated mechanical QA:
  - PNG exists beside source card art.
  - PNG is `1024x1024`.
  - PNG mode is `RGBA`.
  - Alpha extrema include `0` and `255`.
  - All four corner alpha values are `0`.
  - All 16 cells have alpha content.
  - `.png.meta` exists.
  - `.png.meta` contains `spriteMode: 2`.
  - `.png.meta` contains `alphaIsTransparency: 1`.
  - `.png.meta` has 16 direction/frame slice names.
  - `.manifest.json` exists.
  - Manifest row order is `down`, `left`, `right`, `up`.
  - Post-finish visible near-magenta and near-lime pixel counts are `0`.
- Visual QA confirmed row order usable as down/left/right/up and no visible matte, chroma spill, or cutout outline artifacts.

## Finishing Pass Performed

- Removed matte/chroma spill using the imagegen chroma-key helper.
- Applied final low-alpha chroma polish to remove residual `#FF00FF` and lime-like matte pixels from each final sheet.
- Reviewed silhouettes at close zoom through final PNG inspection.

## Cleanup Performed

- No throwaway previews, temporary scripts, or dev logs were created.
- Raw generated-image provenance retained under `C:\Users\yrred\.codex\generated_images\019e2374-ab0d-79c1-9b05-4955f635be23\`.
- Cleaned generated inputs retained under `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-08\` because the manifests reference them.

## Blockers

- None.

## Risks

- Mechanical QA does not prove animation timing quality; Unity or in-engine playback may still reveal motion preferences.
- `def-sackhide-stitchling` repack recorded `component_count: 15`; visual and cell-level QA passed, and the small separated marks reviewed as stitch/bead details rather than matte artifacts.

## Memory-Worthy Notes

- `CU-08` / `cunning` / `rural_agricultural` is complete and marked `QA Passed`.
- Completed creatures: `atk-stubblepicker-stitchling`, `def-sackhide-stitchling`, and `util-rowghost-stitchling`.
- Next pending queue target is `CU-09` / `cunning` / `temperate_forest`.

## Do-Not-Promote Notes

- Do not promote raw generated image IDs unless provenance lookup is needed.
- Do not promote the low-level pixel-polish counts except as evidence that the finishing pass ran.

## Follow-Up Recommendations

- Next automation run should process exactly one package: `CU-09` / `cunning` / `temperate_forest`.
