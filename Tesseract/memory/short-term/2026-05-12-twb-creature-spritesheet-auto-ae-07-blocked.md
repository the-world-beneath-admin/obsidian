# TWB Creature Sprite Sheet Automation Report - AE-07 Blocked

## Task

Automated creature sprite-sheet production worker run for the main game, The World Beneath.

Process exactly one family triad package from the Tier 1 creature walk sprite-sheet queue.

## Lock Status

- Lock acquired with exclusive create-new semantics at `2026-05-12T06:28:21.7253155Z`.
- Lock path: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json`
- No active or stale prior lock was present.
- Intended chunk was updated in the lock to `AE-07 arcane-engineering park`.
- Lock will be released after this report and cleanup step.

## Chunk Processed

- Chunk: AE-07
- Affinity: arcane-engineering
- Biome: park
- Family: Fountainkey Ducks
- Queue status at stop: `Pending`
- Creatures in package:
  - `atk-keybill-duck`
  - `def-coinplate-turtle`
  - `util-fountainchime-sparrow`

## Result

Blocked.

Keybill Duck and Coinplate Turtle were generated, finished, repacked, mechanically QA checked, and visually inspected. Fountainchime Sparrow generation failed: the generated file was a screenshot-like UI image rather than a creature sprite sheet. Per the current automation rule, the run stopped immediately and did not retry or mark the triad complete.

`CHUNK_QUEUE.md` was not modified. AE-07 remains `Pending`.

## Files Touched

Created partial accepted outputs for the first two creatures:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\park\atk-keybill-duck-creature-pet-t1-arcane-engineering-slot10-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\park\atk-keybill-duck-creature-pet-t1-arcane-engineering-slot10-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\park\atk-keybill-duck-creature-pet-t1-arcane-engineering-slot10-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\park\def-coinplate-turtle-creature-pet-t1-arcane-engineering-slot10-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\park\def-coinplate-turtle-creature-pet-t1-arcane-engineering-slot10-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\park\def-coinplate-turtle-creature-pet-t1-arcane-engineering-slot10-def-walk-4dof-1024.manifest.json`

Finished-alpha intermediates retained as provenance for the partial accepted outputs:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\tmp\AE-07\atk-keybill-duck-finished.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\tmp\AE-07\def-coinplate-turtle-finished.png`

Generated source image provenance left in place:

- Accepted Keybill Duck raw sheet: `C:\Users\yrred\.codex\generated_images\019e1ade-9909-75a0-af09-097f98c86fef\ig_04a1a6486f77336f016a02c93a36cc8195bc09ab4b8de9ae51.png`
- Accepted Coinplate Turtle raw sheet: `C:\Users\yrred\.codex\generated_images\019e1ade-9909-75a0-af09-097f98c86fef\ig_04a1a6486f77336f016a02ca87fc8881958d4ef6ef07899afa.png`
- Rejected Fountainchime Sparrow raw output: `C:\Users\yrred\.codex\generated_images\019e1ade-9909-75a0-af09-097f98c86fef\ig_04a1a6486f77336f016a02cc93e6f48195b3194c78827fa8dc.png`

Other files:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-creature-spritesheet-auto-ae-07-blocked.md`

## Checks Run

For Keybill Duck and Coinplate Turtle:

- PNG exists beside source card art.
- PNG size is 1024x1024.
- PNG mode is RGBA.
- Alpha extrema include 0 and 255.
- All four corner alpha values are 0.
- All 16 cells have non-empty alpha content.
- `.png.meta` exists.
- `.png.meta` contains `spriteMode: 2`.
- `.png.meta` contains `alphaIsTransparency: 1`.
- `.png.meta` contains 16 slice names.
- `.manifest.json` exists and records row order as down, left, right, up.
- Final low-alpha chroma sniff found 0 magenta and 0 lime/green edge-dust pixels after cleanup.

Per-creature QA notes:

- Keybill Duck: row order visually reads as down/front, left, right, up/back; no visible matte fringe. Low-alpha chroma dust cleanup removed 142 pixels. Minimum per-cell margins were left 14 px, top 14 px, right 15 px, bottom 12 px.
- Coinplate Turtle: row order visually reads as down/front, left, right, up/back; no visible matte fringe. Low-alpha chroma dust cleanup removed 100 pixels. Minimum per-cell margins were left 13 px, top 30 px, right 13 px, bottom 12 px.

For Fountainchime Sparrow:

- Raw image-generation output was visually inspected and rejected before repack.
- No final Sparrow PNG, `.png.meta`, or `.manifest.json` was created.

## Finishing Pass Performed

For Keybill Duck and Coinplate Turtle:

- Used flat magenta `#FF00FF` matte in the generation prompt.
- Removed magenta matte with soft matte, edge contract, and despill.
- Repacked through `tools\art\repack_creature_walk_sheet.py`.
- Performed final low-alpha chroma dust cleanup on the repacked PNG.
- Reran mechanical QA and visual QA after cleanup.

For Fountainchime Sparrow:

- No finishing pass was performed because the raw generated output failed before post-processing.

## Cleanup Performed

- No broad cleanup, revert, or source-file deletion was run.
- No source art, raw generated-image provenance, reports, or other worker files were deleted.
- Finished-alpha intermediates for Keybill Duck and Coinplate Turtle were retained because their manifests reference them as repack input provenance.
- No throwaway preview files were created.

## Blockers

- Fountainchime Sparrow image generation produced a screenshot-like UI image rather than a 4x4 creature sprite sheet.
- Current automation rules require stopping on a failed or ambiguous creature in the package, so AE-07 cannot be marked complete in this run.

## Risks

- AE-07 now has two partial accepted outputs in the folder while the queue row remains `Pending`. A future run should detect and reuse or verify these rather than blindly overwriting them.
- The Sparrow generation failure may have been caused by image-generation context contamination after multiple local image views and tool outputs. A future run may need to re-open only the Sparrow source image immediately before generation, or use a cleaner fresh image-generation context.
- Mechanical QA does not prove in-engine animation feel for the two partial outputs.

## Memory-Worthy Notes

- AE-07 is blocked, not complete.
- Keybill Duck and Coinplate Turtle partial outputs passed mechanical and visual QA.
- Fountainchime Sparrow raw output was rejected before repack because it was not a sprite sheet.
- The queue remains `Pending` and was not updated.

## Do-Not-Promote Notes

- Do not promote the rejected Sparrow generated image as creature art, sprite-sheet output, or canon reference.
- Do not promote AE-07 as complete until all three creatures pass QA and `CHUNK_QUEUE.md` is updated.

## Follow-Up Recommendations

- Next automation run should handle AE-07 / arcane-engineering / park, starting with a clear decision on whether to reuse the already accepted Keybill Duck and Coinplate Turtle outputs or regenerate the full triad.
- For Sparrow, isolate image-generation context before retrying and verify the raw output is a 4x4 creature sheet before any finishing pass.
