# 2026-05-13 TWB Creature Sprite Sheet - Chuck

## Task

Create a one-off 4-direction walk sprite sheet for Chuck from:

`C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-chuck-creature-special-ephemrial-spirit-chuck.png`

Scope: Main game / The World Beneath art pipeline.

## Result

Completed Chuck's sibling walk sheet assets:

- `def-chuck-creature-special-ephemrial-spirit-chuck-walk-4dof-1024.png`
- `def-chuck-creature-special-ephemrial-spirit-chuck-walk-4dof-1024.png.meta`
- `def-chuck-creature-special-ephemrial-spirit-chuck-walk-4dof-1024.manifest.json`

The final sheet is a 1024x1024 RGBA 4x4 grid with row order visually usable as down, left, right, up.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-chuck-creature-special-ephemrial-spirit-chuck-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-chuck-creature-special-ephemrial-spirit-chuck-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\def-chuck-creature-special-ephemrial-spirit-chuck-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\Special-alpha-sources\def-chuck-alpha.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-creature-spritesheet-chuck.md`

Generated-image provenance was created by the image generation tool and preserved under:

`C:\Users\yrred\.codex\generated_images\019e1a4d-4e09-76f1-abdb-8b4720d05bf4\ig_0625cfc5c57cdf39016a04ab1546488195823556c7f5a91413.png`

## Checks run

- Inspected the Chuck source PNG before generation.
- Generated a full 4x4 walk sheet using Chuck's source identity as the lock.
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
  - `.png.meta` exists.
  - `.png.meta` contains `spriteMode: 2`.
  - `.png.meta` contains `alphaIsTransparency: 1`.
  - `.png.meta` has 16 slice names.
  - `.manifest.json` exists.
  - Manifest row order is down, left, right, up.
  - Manifest frame count is 4 per direction.
  - Manifest component count is 16.

## Cleanup performed

No disposable scratch files or throwaway logs were created. The generated-image provenance and alpha source were retained as production evidence.

## Risks

- The generated walk cycle is AI-derived rather than hand-authored; it is usable for the current sprite-sheet pass but may still benefit from animator polish later.
- The side and back rows preserve the character identity and direction readability, but motion variation is subtle.

## Memory-worthy notes

- Chuck's special companion walk sheet is complete using the same source-lock, magenta-matte cleanup, and repack workflow used for Stanly, Hazel, and Merlin.
- The existing folder spelling `ephemrial_spirit` was preserved.

## Do not promote to memory

- Do not promote the generated-image provenance path as durable project knowledge.
- Do not promote the one-off QA command details unless they become part of a reusable automation note.

## Follow-up recommendations

- Continue producing special companion sheets one creature at a time from approved source art.
- Consider a later animation-polish pass if these special companion walk cycles become prominent in gameplay.
