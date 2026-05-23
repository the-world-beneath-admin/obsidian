# Working Window Intake - 2026-05-12 - TWB Creature Sprite Sheets

## Project Identity
- Project/window name: TWB Creature Sprite Sheets
- Main goal: Produce Unity-ready 4-direction creature walk sprite sheets for the Tier 1 pet card-art system, filed beside each source creature art asset.
- Scope: Current window focused on documentation, repeatable tooling, and the first main pet chunks of the sprite-sheet conversion pass.
- Code/project directory: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`
- Related Obsidian lane, if known: Not confirmed. Suggested lane: TWB art pipeline / creature animation assets.
- Suggested future worker role name: `twb-creature-spritesheet-worker`

## Current State
The sprite-sheet workflow has been established and used on multiple creatures.

Completed so far:
- A repeatable guide exists for generating per-creature 4-direction sprite sheets.
- A top-level Codex usage guide exists for wiring these sheets into game/runtime work later.
- A local repacking helper exists and writes final PNG, Unity `.png.meta`, and `.manifest.json` files beside each source card-art PNG.
- Main chunk `AE-01` / `arcane-engineering` / `boreal_forest` is complete and marked `QA Passed`.
- Main chunk `AE-02` / `arcane-engineering` / `desert` is complete and marked `QA Passed`.
- Main chunk `AE-03` / `arcane-engineering` / `freshwater` is complete and marked `QA Passed`.
- Special Peggy sheet is complete beside the existing Peggy card-art folder.

Currently in progress:
- No active implementation should continue until Bob/orchestrator reviews this short-term intake.

Not yet started:
- `AE-04` and all later queue chunks.
- Permanent Obsidian memory promotion.
- Unity runtime wiring/import verification inside the editor.
- HyperFrames preview generation for the newest chunks.

## Files And Areas Touched
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\art\repack_creature_walk_sheet.py`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\CREATURE_WALK_SPRITESHEET_USAGE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\T1_CREATURE_WALK_SPRITESHEET_HOWTO.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\boreal_forest\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\desert\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\freshwater\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\`
- Generated image sources remained under `C:\Users\yrred\.codex\generated_images\019e199a-f4f8-7a21-8906-dedef29d457a\`.

Completed main chunk sheets:
- `atk-latchbite-marten`, `def-snowbracket-hare`, `util-hingecall-jay`
- `atk-lensnip-gecko`, `def-shadeplate-tortoise`, `util-sunspool-jerboa`
- `atk-pinchmark-newt`, `def-valveback-turtle`, `util-ripplegear-minnow`

Completed special sheet:
- `util-peggy-creature-special-ephemrial-spirit-peggy`

## Decisions Made
- Decision - Final walk sheets are filed beside their matching card-art PNG in the existing `.md\T1_Creature_Art_Prompt_System\affinities\<affinity>\<biome>\` hierarchy, not in a central animation folder.
- Source - User instruction to keep completed sheets next to proper art in the same structured filing system.

- Decision - Walk sheet naming strips only a terminal version suffix like `-v2`, then appends `-walk-4dof-1024`.
- Source - Workflow guide and implemented repacker behavior.

- Decision - Standard sheet contract is `1024x1024`, `4x4`, `256x256` cells, row order `down`, `left`, `right`, `up`, 4 frames per direction.
- Source - User request for 4 DOF walk sheets and established guide.

- Decision - Unity metadata is generated as `Sprite (2D and UI)`, `Multiple`, bottom-center pivot `{x: 0.5, y: 0.08}`, no mipmaps, no compression, alpha transparency enabled.
- Source - Repacker output contract and top-level usage guide.

- Decision - Ripplegear Minnow uses a swim/hover walk-equivalent while keeping the same 4-direction sheet layout.
- Source - Practical interpretation during AE-03, because the source is a fish and should not be given legs.

- Decision - Peggy was filed under the actual existing folder `special\ephemrial_spirit`, not the user-provided `special\guardian_angels` path.
- Source - Local filesystem search found Peggy only under `special\ephemrial_spirit`.

## Memory-Worthy Facts
- Fact - The main sprite-sheet queue is organized as `117` family triad chunks of 3 creatures each: `atk`, `def`, and `util`.
- Source - `Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`

- Fact - Chunks `AE-01`, `AE-02`, and `AE-03` are complete and marked `QA Passed`.
- Source - `Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`

- Fact - Every completed final sheet should have three sibling files: `.png`, `.png.meta`, and `.manifest.json`.
- Source - `CREATURE_WALK_SPRITESHEET_USAGE.md` and generated outputs.

- Fact - The local repacker is the current canonical post-process helper for generated 4x4 sheets.
- Source - `tools\art\repack_creature_walk_sheet.py`

- Fact - Generated source images from the built-in image tool are not the project assets; final project assets are the repacked sheets beside source art.
- Source - Image generation workflow and file placement policy.

- Fact - The creature source image is the identity lock for each generation.
- Source - `.md\T1_Creature_Art_Prompt_System\T1_CREATURE_WALK_SPRITESHEET_HOWTO.md`

## Risks / Warnings
- Warning - The repo working tree is very dirty with many unrelated modified, deleted, and untracked files. Future workers must avoid broad cleanup or revert operations.
- Warning - The `.md` art folders appear untracked in Git status, so `git status --short` may show entire folders as `??` rather than individual new sheets.
- Warning - Built-in image generation often shows a checkerboard-looking background; the repacker removes edge checker/chroma backgrounds and validates true alpha, but visual QA is still required.
- Warning - Some generated rows may be visually acceptable but not perfect animation cycles. Mechanical QA does not prove motion quality.
- Warning - Special folder names may contain existing misspellings such as `ephemrial_spirit`; preserve the real folder unless a deliberate migration is planned.
- Warning - Do not delete generated source images from `C:\Users\yrred\.codex\generated_images\...`; they are provenance for manifests and may aid regeneration.
- Warning - Unity editor import has not been manually verified for the newest chunks, only `.meta` content and image properties were checked.

## Open Questions
- Should the completed walk sheets eventually be mirrored or imported into an `Assets/` runtime folder, or should Unity consume them from the current `.md` hierarchy?
- Should fish, birds, and other non-walking creatures continue to use the same `walk-4dof` naming, or should the runtime later map them to `swim` / `fly` semantics while preserving the same sheet grid?
- Should every chunk get a HyperFrames preview, or only questionable creatures and milestone batches?
- Should `ephemrial_spirit` be corrected globally later, or preserved forever as an established project identifier?
- What is the target Unity runtime loader path and naming lookup strategy for these sheets?

## Do Not Promote
- Do not promote raw generated image file names as canonical asset paths.
- Do not promote the temporary idea that `guardian_angels` is Peggy's actual folder.
- Do not promote checkerboard backgrounds as acceptable final transparency.
- Do not promote visual judgement that any sheet is final beyond the stated QA pass; art direction can still request regeneration.
- Do not promote unrelated dirty Git status noise from the wider Unity project as part of this sprite-sheet task.

## Current Blockers
- No technical blocker for continuing the next chunk after orchestrator review.
- Bob/orchestrator review is the current process gate because the user requested implementation pause after writing this intake.

## Checks Run
- Visual source inspection using image viewing for source card art and generated/repacked sheets.
- Repacker execution for each completed sheet using `python tools\art\repack_creature_walk_sheet.py --source ... --generated ...`.
- Python/Pillow QA checks for final sheets:
  - PNG size exactly `(1024, 1024)`
  - mode `RGBA`
  - alpha extrema include `0` and `255`
  - all four corner alpha values are `0`
  - every `256x256` cell has non-empty alpha content
  - `.png.meta` exists
  - `.manifest.json` exists
  - `.png.meta` contains `spriteMode: 2`
  - `.png.meta` contains `alphaIsTransparency: 1`
  - `.png.meta` has `16` slice name lines
- `git status --short -- <target folders>` checks were run for touched art folders and queue files.

## Cleanup Needed
- Generated source images under `C:\Users\yrred\.codex\generated_images\019e199a-f4f8-7a21-8906-dedef29d457a\` can be kept for provenance; do not delete unless explicitly instructed.
- The broader Unity repo has many unrelated dirty changes and deletions that should be handled separately from sprite-sheet production.
- If disk space becomes a problem, review generated image cache policy with the user before deleting anything.
- Unity may generate or update additional `.meta` files if these art folders are imported or moved later.

## Recommended Obsidian Tree
- `memory/wiki/twb-creature-spritesheets/overview.md`
- `memory/wiki/twb-creature-spritesheets/asset-contract.md`
- `memory/wiki/twb-creature-spritesheets/decisions.md`
- `memory/wiki/twb-creature-spritesheets/open-questions.md`
- `memory/reports/twb-creature-spritesheets/`
- `memory/short-term/`

## Recommended Worker Agent
- Agent name: `twb-creature-spritesheet-worker`
- Purpose: Continue chunk-by-chunk generation, repacking, visual QA, mechanical QA, and queue updates for Tier 1 pet walk sprite sheets.
- Read-first files:
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\CREATURE_WALK_SPRITESHEET_USAGE.md`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\T1_CREATURE_WALK_SPRITESHEET_HOWTO.md`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\art\repack_creature_walk_sheet.py`
- Allowed write paths:
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\`
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\output\hyperframes\` only when previews are explicitly requested.
- Forbidden write paths:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\` unless orchestrator explicitly promotes memory.
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
  - Broad Unity code folders outside the art pipeline unless explicitly assigned.
- Done criteria:
  - Each creature in the assigned chunk has a sibling `-walk-4dof-1024.png`, `.png.meta`, and `.manifest.json`.
  - Final PNG is `1024x1024`, `RGBA`, true transparent, and all cells populated.
  - Visual inspection confirms no cropping and row order is usable as `down`, `left`, `right`, `up`.
  - Unity `.meta` contains `spriteMode: 2`, `alphaIsTransparency: 1`, and `16` slice names.
  - Chunk queue is updated only after all three creatures pass QA.
  - Final user report lists completed paths and checks.
- Report destination: `memory/short-term/`

## Next Recommended Gate
Bob/orchestrator should review this intake, decide what becomes permanent Obsidian memory, then authorize the next implementation step. The next production action, if approved, is to begin `AE-04` / `arcane-engineering` / `grassland`.
