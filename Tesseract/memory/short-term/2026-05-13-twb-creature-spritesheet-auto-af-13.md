# TWB Creature Spritesheet Automation - AF-13

- Task: TWB Sprite Sheet Single Runner for one family triad package.
- Run time: 2026-05-13T09:47:52.2690505-05:00.
- Lock status: Acquired with create-new semantics; intended chunk updated to `AF-13`; lock path `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json`.
- Chunk processed: `AF-13` / `arcane-fighting` / `urban_residential` / Lotline Wardkin.
- Result: Complete. All three creatures generated, magenta-chroma-cleaned, alpha-bled, repacked, finishing-pass cleaned, visually inspected, mechanically QA-passed, and `CHUNK_QUEUE.md` updated to `QA Passed`.

## Creatures Completed

- `atk-signspike-opossum` -> `atk-signspike-opossum-creature-pet-t1-arcane-fighting-slot13-atk-walk-4dof-1024.png`
- `def-hedgeward-skunk` -> `def-hedgeward-skunk-creature-pet-t1-arcane-fighting-slot13-def-walk-4dof-1024.png`
- `util-gutterring-eft` -> `util-gutterring-eft-creature-pet-t1-arcane-fighting-slot13-util-walk-4dof-1024.png`

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\atk-signspike-opossum-creature-pet-t1-arcane-fighting-slot13-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\atk-signspike-opossum-creature-pet-t1-arcane-fighting-slot13-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\atk-signspike-opossum-creature-pet-t1-arcane-fighting-slot13-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\def-hedgeward-skunk-creature-pet-t1-arcane-fighting-slot13-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\def-hedgeward-skunk-creature-pet-t1-arcane-fighting-slot13-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\def-hedgeward-skunk-creature-pet-t1-arcane-fighting-slot13-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\util-gutterring-eft-creature-pet-t1-arcane-fighting-slot13-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\util-gutterring-eft-creature-pet-t1-arcane-fighting-slot13-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-fighting\urban_residential\util-gutterring-eft-creature-pet-t1-arcane-fighting-slot13-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AF-13_chroma_cleaned_sources\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- Raw generated-image provenance retained under `C:\Users\yrred\.codex\generated_images\019e21b5-4928-7793-b502-9d75a9f64e0b\`.

## Checks Run

- Source card-art identity inspected for all three creatures.
- Built-in image generation used once per creature, requesting flat `#FF00FF` as the only temporary chroma matte.
- `remove_chroma_key.py` used with border-sampled magenta cleanup, soft matte, and despill.
- Alpha clamp and alpha-bleed finishing source pass performed before each repack.
- Project repacker run for each creature to create final PNG, `.png.meta`, and `.manifest.json` beside the source card art.
- Final alpha clamp and alpha bleed performed after repack to remove resize dust and hidden chroma RGB.
- Combined mechanical QA passed for all three: `1024x1024`, `RGBA`, alpha extrema `0/255`, all four corner alpha values `0`, all `16` cells populated, `.png.meta` exists, `spriteMode: 2`, `alphaIsTransparency: 1`, `16` unique slice names, `.manifest.json` exists, and manifest row order is `down/left/right/up`.
- Exact key-color artifact scan passed for all three: zero visible pixels within threshold of magenta `#FF00FF` or lime `#00FF00` after the finishing pass.
- Visual QA performed on dark-background composites and close working previews: rows read as down/front, left, right, up/back; identities and role silhouettes remained readable; no visible matte, chroma fringe, or cutout outline artifacts remained.

## Finishing Pass Performed

- Removed generated magenta gradient matte with local chroma cleanup.
- Despilled chroma-key contamination and clamped tiny alpha haze.
- Applied alpha bleed around sprite edges before repack and after final repack.
- Removed alpha-1/alpha-2 chroma dust from resized edges.
- Preserved intentional red/cyan sigil markings, eyes, charms, leaves/moss, armor, fur stripes, pale highlights, and native pixel-art outlines.

## Cleanup Performed

- Removed temporary `*-generated-bgclean.png` pre-bleed files.
- Removed temporary dark-background QA preview composites, key-color overlay previews, and the combined visual-check image after inspection.
- Retained final cleaned source evidence in `AF-13_chroma_cleaned_sources`.
- Retained raw generated images under `.codex\generated_images`.
- No source card art, raw generated images, reports, or other worker output was deleted.

## Blockers

- None.

## Risks

- The generator again produced magenta gradients despite flat-matte prompting. Local cleanup handled them, but future runs should continue using chroma removal, alpha clamp, and alpha bleed before and after repack.
- These creatures contain intentional red/cyan sigils and green leaf/moss accents; broad color scans can falsely flag them. Exact key-color scans plus dark-background visual QA are more reliable.

## Memory-Worthy Notes

- `AF-13` / `arcane-fighting` / `urban_residential` is complete and `QA Passed` with `atk-signspike-opossum`, `def-hedgeward-skunk`, and `util-gutterring-eft`.
- Arcane Fighting is now complete through `AF-13`.
- Next pending package is `CU-01` / `cunning` / `boreal_forest`.
- The magenta matte plus chroma-clean/alpha-bleed finishing path remained viable for the Lotline Wardkin set.

## Do-Not-Promote Notes

- Do not treat retained `AF-13_chroma_cleaned_sources` files as final Unity assets.
- Do not promote raw generated images as final assets; they are provenance only and originally contained magenta matte backgrounds.
- Do not treat intentional red/cyan sigils, green leaf/moss accents, pale fur/belly highlights, or dark pixel-art outlines as matte artifacts by themselves.

## Follow-Up Recommendations

- Next run should process exactly one package: `CU-01` / `cunning` / `boreal_forest`.
- Keep using singleton lock, magenta-only temporary matte prompts, chroma removal, alpha clamp, alpha bleed, exact key-color scan, and close visual edge QA.
