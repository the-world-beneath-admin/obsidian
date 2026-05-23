# Task

Continue the Tier 1 creature walk sprite-sheet production pass for `AE-04` / `arcane-engineering` / `grassland`.

Scope: Main game / The World Beneath art pipeline.

Target creatures:

- `atk-vaneclaw-hopper-creature-pet-t1-arcane-engineering-epsilon-atk.png`
- `def-kiteplate-prairie-dog-creature-pet-t1-arcane-engineering-epsilon-def.png`
- `util-weatherbell-lark-creature-pet-t1-arcane-engineering-epsilon-util.png`

# Result

Completed all three AE-04 walk sheets. Each target creature now has a sibling `-walk-4dof-1024.png`, `.png.meta`, and `.manifest.json` beside the source card-art PNG.

`CHUNK_QUEUE.md` was updated to mark `AE-04` as `QA Passed` only after all three creatures passed mechanical and visual QA.

# Files touched

Final sprite assets:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\atk-vaneclaw-hopper-creature-pet-t1-arcane-engineering-epsilon-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\atk-vaneclaw-hopper-creature-pet-t1-arcane-engineering-epsilon-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\atk-vaneclaw-hopper-creature-pet-t1-arcane-engineering-epsilon-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\def-kiteplate-prairie-dog-creature-pet-t1-arcane-engineering-epsilon-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\def-kiteplate-prairie-dog-creature-pet-t1-arcane-engineering-epsilon-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\def-kiteplate-prairie-dog-creature-pet-t1-arcane-engineering-epsilon-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\util-weatherbell-lark-creature-pet-t1-arcane-engineering-epsilon-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\util-weatherbell-lark-creature-pet-t1-arcane-engineering-epsilon-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\grassland\util-weatherbell-lark-creature-pet-t1-arcane-engineering-epsilon-util-walk-4dof-1024.manifest.json`

Stable processed generation sources:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AE-04-alpha-sources\atk-vaneclaw-hopper-alpha.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AE-04-alpha-sources\def-kiteplate-prairie-dog-alpha.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AE-04-alpha-sources\util-weatherbell-lark-alpha.png`

Queue/report files:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-creature-spritesheet-ae-04.md`

# Checks run

- Inspected the three source card-art PNGs before generation.
- Generated one full 4x4 sheet per creature using the source image as identity lock.
- Removed the flat magenta chroma-key background with `remove_chroma_key.py`.
- Repacked each cleaned sheet with `tools\art\repack_creature_walk_sheet.py`.
- Visually inspected each final `1024x1024` sheet for source identity, row order, cropping, and usable walk/hop cycles.
- Ran a Python QA pass confirming, for each final sheet:
  - PNG exists.
  - PNG size is `1024x1024`.
  - PNG mode is `RGBA`.
  - Alpha extrema include `0` and `255`.
  - All four corner alpha values are `0`.
  - Every `256x256` cell has non-empty alpha content.
  - `.png.meta` exists.
  - `.png.meta` contains `spriteMode: 2`.
  - `.png.meta` contains `alphaIsTransparency: 1`.
  - `.png.meta` has `16` sprite slice names.
  - `.manifest.json` exists.
  - Manifest row order is `down`, `left`, `right`, `up`.
  - Manifest generated-source paths exist.

# Cleanup performed

- Deleted the temporary working folder `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\ae-04-temp`.
- Preserved original generated image provenance under `C:\Users\yrred\.codex\generated_images\019e1a4d-4e09-76f1-abdb-8b4720d05bf4`.
- Preserved cleaned alpha source sheets under `AE-04-alpha-sources` because the final manifests reference them.

# Risks

- These are AI-generated walk/hop cycles, so motion quality still benefits from in-engine preview before runtime use.
- The lark uses a walk-equivalent hop/flap interpretation because bird movement is not semantically separate from `walk-4dof` yet.
- Minor pose and equipment simplification occurs across generated direction rows, but the key source identities remain readable.

# Memory-worthy notes

- `AE-04` / `arcane-engineering` / `grassland` is complete and marked `QA Passed`.
- Chroma-key outputs needed explicit matte cleanup before repacking; direct repack from raw magenta sheets left visible edge contamination.
- Stable cleaned alpha sources were retained in `Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AE-04-alpha-sources` so manifests do not point to deleted temporary files.

# Do not promote to memory

- Individual generated-image filenames and prompt wording are not durable project knowledge.
- The deleted temporary `ae-04-temp` path is not durable project knowledge.
- One-off visual quirks from this generation pass should not be promoted unless repeated in later chunks.

# Follow-up recommendations

- Continue with `AE-05` / `arcane-engineering` / `industrial` as the next bounded triad if the same production lane remains active.
- Consider adding chroma-key cleanup as a documented pre-repack step for future generated sheets.
- Consider a lightweight in-engine or HyperFrames preview milestone after several chunks to catch motion-jitter issues not visible in static sheet QA.
