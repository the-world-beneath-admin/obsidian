# Task

Create a Unity-ready four-direction walk sprite sheet for Merlin only.

Scope: Main game / The World Beneath art pipeline.

Source:

`C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-merlin-creature-special-ephemrial-spirit-merlin.png`

# Result

Completed Merlin's walk sprite sheet beside the source card art.

Final output:

`C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-merlin-creature-special-ephemrial-spirit-merlin-walk-4dof-1024.png`

No chunk queue was updated because this was a one-off special creature request, not a queued triad.

The existing `current-game-dev-task.md` was not overwritten because it is currently assigned to an unrelated main-game world-map UI task.

# Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-merlin-creature-special-ephemrial-spirit-merlin-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-merlin-creature-special-ephemrial-spirit-merlin-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\special\ephemrial_spirit\atk-merlin-creature-special-ephemrial-spirit-merlin-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\Special-alpha-sources\atk-merlin-alpha.png`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-creature-spritesheet-merlin.md`

# Checks run

- Inspected Merlin's source PNG before generation.
- Read Merlin's source prompt and preserved the key identity features: large black-and-white Maine Coon, long shaggy fur, heavy body, white chest ruff, white muzzle/blaze, white paws, green aloof hunter eyes, long whiskers, full plume tail, and chitter-before-pounce energy.
- Generated a single 4x4 full-sheet pass using the built-in image generation workflow.
- Used flat magenta `#FF00FF` as the temporary matte.
- Removed the matte with `remove_chroma_key.py` using soft matte, despill, and edge contraction.
- Repacked the cleaned source with `tools\art\repack_creature_walk_sheet.py` at `--content-limit 205` for safer plume-tail padding.
- Visually inspected the final sheet for identity, row order, cropping, and matte fringe.
- Ran Python QA confirming:
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
  - Manifest generated-source path exists.

# Cleanup performed

- No temporary project folder was created for this pass.
- Preserved original generated image provenance under `C:\Users\yrred\.codex\generated_images\019e1a4d-4e09-76f1-abdb-8b4720d05bf4`.
- Preserved the cleaned alpha source at `Special-alpha-sources\atk-merlin-alpha.png` because the manifest references it.

# Risks

- Generated walk cycles still need in-engine preview to judge motion polish and frame-to-frame rhythm.
- Merlin's tail and long fur required conservative scaling; the final sheet favors safe padding over maximum sprite size.
- The subtle teal wisps are retained as body-local Cunning/Ephemrial Spirit accents; runtime review may decide whether to reduce that effect.

# Memory-worthy notes

- Merlin now has a completed special-creature walk sheet in `affinities\special\ephemrial_spirit`.
- The existing `ephemrial_spirit` spelling was preserved intentionally.
- A repack content limit of `205` worked for Merlin's heavy Maine Coon body and plume tail.

# Do not promote to memory

- The raw generated-image filename and prompt wording are not durable project memory.
- One-off matte cleanup settings should not be promoted unless repeated in future special-creature passes.

# Follow-up recommendations

- Preview Merlin in Unity or a simple animation viewer before wiring him into runtime use.
- If more special starter companions are produced, consider a small special-companion queue separate from the Tier 1 triad queue.
