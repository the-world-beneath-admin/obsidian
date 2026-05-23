# 2026-05-13 TWB Creature Sprite Sheet - Nova

## Task

Create a one-off 4-direction walk sprite sheet for Nova from:

`C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-nova-creature-special-ephemrial-spirit-nova.png`

Scope: Main game / The World Beneath art pipeline.

## Result

Completed Nova's sibling walk sheet assets:

- `def-nova-creature-special-ephemrial-spirit-nova-walk-4dof-1024.png`
- `def-nova-creature-special-ephemrial-spirit-nova-walk-4dof-1024.png.meta`
- `def-nova-creature-special-ephemrial-spirit-nova-walk-4dof-1024.manifest.json`

The final sheet is a 1024x1024 RGBA 4x4 grid with row order visually usable as down, left, right, up.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-nova-creature-special-ephemrial-spirit-nova-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-nova-creature-special-ephemrial-spirit-nova-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-nova-creature-special-ephemrial-spirit-nova-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\Special-alpha-sources\def-nova-alpha.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-creature-spritesheet-nova.md`

Generated-image provenance was created by the image generation tool and preserved under:

`C:\Users\yrred\.codex\generated_images\019e1a4d-4e09-76f1-abdb-8b4720d05bf4\ig_0625cfc5c57cdf39016a04adfb08cc8195a33aae44ca448c1b.png`

## Checks run

- Read project memory scope files and Nova's local prompt.
- Inspected the Nova source PNG before generation.
- Generated a full 4x4 walk sheet using Nova's source identity as the lock.
- Removed the flat `#FF00FF` matte with:
  - `remove_chroma_key.py`
  - `--soft-matte`
  - `--despill`
  - `--edge-contract 2`
- Repacked with:
  - `repack_creature_walk_sheet.py`
  - `--content-limit 210`
- Visually inspected the alpha-clean intermediate sheet.
- Visually inspected the final 1024x1024 packed sheet.
- Ran formal PNG/meta/manifest QA:
  - PNG exists beside source art.
  - PNG size is exactly 1024x1024.
  - PNG mode is RGBA.
  - Alpha extrema are 0 and 255.
  - All four corner alpha values are 0.
  - Every 256x256 cell has non-empty alpha content.
  - Minimum per-cell alpha margin is 12 px.
  - `.png.meta` exists.
  - `.png.meta` contains `spriteMode: 2`.
  - `.png.meta` contains `alphaIsTransparency: 1`.
  - `.png.meta` has 16 slice names.
  - `.manifest.json` exists.
  - Manifest row order is down, left, right, up.
  - Manifest frame count is 4 per direction.

## Cleanup performed

No disposable scratch files or throwaway logs were created. The generated-image provenance and alpha source were retained as production evidence.

## Risks

- The generated walk cycle is AI-derived rather than hand-authored; it is usable for the current sprite-sheet pass but may still benefit from animator polish later.
- The repacker reported `component_count: 17` because Nova's spirit-wisp/sparkle accents include detached alpha components. Final QA still passed with all 16 cells populated and visible row order intact.
- Side-view motion is subtle, especially in the body; the paws, ears, ward charm, and wisps carry most of the frame-to-frame read.

## Memory-worthy notes

- Nova's special companion walk sheet is complete using the same source-lock, magenta-matte cleanup, and repack workflow used for the other special companions.
- The existing folder spelling `ephemrial_spirit` was preserved.
- Nova's identity lock should preserve black tri-color corgi markings, upright ears, white chest/paws/blaze, gold ward charm, and pale-blue spirit wisps.

## Do not promote to memory

- Do not promote the generated-image provenance path as durable project knowledge.
- Do not promote the one-off QA command details unless they become part of a reusable automation note.

## Follow-up recommendations

- Continue producing special companion sheets one creature at a time from approved source art.
- Consider a later animation-polish pass if these special companion walk cycles become prominent in gameplay.
