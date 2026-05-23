# TWB Creature Spritesheet Automation - AF-12

- Task: TWB Sprite Sheet Single Runner for one family triad package.
- Run time: 2026-05-13T08:42:43.7253365-05:00.
- Lock status: Acquired with create-new semantics at `2026-05-13T13:20:52.2947359Z`; intended chunk updated to `AF-12`.
- Chunk processed: `AF-12` / `arcane-fighting` / `urban_commercial` / Glassline Scavengers.
- Result: Complete. All three creatures generated, magenta-chroma-cleaned, alpha-bled, repacked, finishing-pass cleaned, visually inspected, mechanically QA-passed, and `CHUNK_QUEUE.md` updated to `QA Passed`.

## Creatures Completed

- `atk-signlash-crow` -> `atk-signlash-crow-creature-pet-t1-arcane-fighting-slot12-atk-walk-4dof-1024.png`
- `def-shuttermask-raccoon` -> `def-shuttermask-raccoon-creature-pet-t1-arcane-fighting-slot12-def-walk-4dof-1024.png`
- `util-waymark-pigeon` -> `util-waymark-pigeon-creature-pet-t1-arcane-fighting-slot12-util-walk-4dof-1024.png`

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\atk-signlash-crow-creature-pet-t1-arcane-fighting-slot12-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\atk-signlash-crow-creature-pet-t1-arcane-fighting-slot12-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\atk-signlash-crow-creature-pet-t1-arcane-fighting-slot12-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\def-shuttermask-raccoon-creature-pet-t1-arcane-fighting-slot12-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\def-shuttermask-raccoon-creature-pet-t1-arcane-fighting-slot12-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\def-shuttermask-raccoon-creature-pet-t1-arcane-fighting-slot12-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\util-waymark-pigeon-creature-pet-t1-arcane-fighting-slot12-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\util-waymark-pigeon-creature-pet-t1-arcane-fighting-slot12-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_commercial\util-waymark-pigeon-creature-pet-t1-arcane-fighting-slot12-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AF-12_chroma_cleaned_sources\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- Raw generated-image provenance retained under `C:\Users\yrred\.codex\generated_images\019e217e-3bfc-7e60-a13d-2799f4ebd878\`.

## Checks Run

- Source card-art identity inspected for all three creatures.
- Built-in image generation used once per creature, requesting flat `#FF00FF` as the only temporary chroma matte.
- `remove_chroma_key.py` used with border-sampled magenta cleanup, soft matte, and despill.
- Alpha clamp and alpha-bleed finishing source pass performed before each repack.
- Project repacker run for each creature to create final PNG, `.png.meta`, and `.manifest.json` beside the source card art.
- Combined mechanical QA passed for all three: `1024x1024`, `RGBA`, alpha extrema `0/255`, all four corner alpha values `0`, all `16` cells populated, `.png.meta` exists, `spriteMode: 2`, `alphaIsTransparency: 1`, `16` slice names, `.manifest.json` exists, and manifest row order is `down/left/right/up`.
- Edge-artifact scan passed for all three: zero visible magenta-like pixels and zero visible green/lime-like pixels after finishing.
- Visual QA performed on finished alpha composites and close zoom: rows read as down/front, left, right, up/back; identities and role silhouettes remained readable; no visible matte, chroma fringe, or cutout outline artifacts remained.

## Finishing Pass Performed

- Removed generated magenta gradient matte with local chroma cleanup.
- Removed cutout spill and clamped tiny alpha haze.
- Applied alpha bleed around sprite edges before repack and after final repack to avoid hidden magenta RGB contaminating resized edges.
- Preserved intentional red/cyan sigil markings, crystals, beads, feathers, armor, tail markings, and native pixel-art outlines.

## Cleanup Performed

- Removed temporary `*-generated-bgclean.png` pre-bleed files.
- Removed temporary dark-background QA preview composites and close-zoom composite after inspection.
- Retained final cleaned source evidence in `AF-12_chroma_cleaned_sources`.
- Retained raw generated images under `.codex\generated_images`.
- No source card art, raw generated images, reports, or other worker output was deleted.

## Blockers

- None.

## Risks

- The generator again produced magenta gradients despite flat-matte prompting. Local cleanup handled them, but future runs should continue using chroma removal plus alpha bleed before repack.
- The utility creature uses a light body and pale wing, so future reviews should not misclassify intentional pale highlights as white matte fringe without compositing over a dark background first.

## Memory-Worthy Notes

- `AF-12` / `arcane-fighting` / `urban_commercial` is complete and `QA Passed` with `atk-signlash-crow`, `def-shuttermask-raccoon`, and `util-waymark-pigeon`.
- Next pending package is `AF-13` / `arcane-fighting` / `urban_residential`.
- The magenta matte plus chroma-clean/alpha-bleed finishing path remained viable for the Glassline Scavengers set.

## Do-Not-Promote Notes

- Do not treat the retained `AF-12_chroma_cleaned_sources` files as final Unity assets.
- Do not promote raw generated images as final assets; they still contain magenta matte backgrounds.
- Do not treat intentional red/cyan route marks, pale feather highlights, crystal accents, or dark pixel-art outlines as matte artifacts by themselves.

## Follow-Up Recommendations

- Next run should process exactly one package: `AF-13` / `arcane-fighting` / `urban_residential`.
- Keep using singleton lock, magenta-only temporary matte prompts, chroma removal, alpha bleed, and close visual edge QA.
