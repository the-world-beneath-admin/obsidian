# TWB Creature Spritesheet Automation - AE-08 Blocker

- Task: Automated TWB creature sprite-sheet production worker for The World Beneath.
- Scope: Main game / The World Beneath.
- Run time: 2026-05-12T03:53:05.3420855-05:00
- Lock status: Acquired before queue selection; intended chunk set to AE-08 arcane-engineering/rural_agricultural; released after report and cleanup.
- Chunk processed: AE-08 / arcane-engineering / rural_agricultural / Millmark Barnlings.
- Queue status: Not updated; AE-08 remains Pending.

## Result

Blocked after the second creature. atk-crankspur-rooster passed mechanical QA, finishing cleanup, and visual sniff test, and its final Unity assets remain beside the source art. def-chaffplate-goat failed visual QA after repack because the generated matte was not truly flat and background residue caused the repacker to shrink frames severely. util-pulleywhisker-mouse was not attempted.

## Files Touched

Created and retained:

- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\rural_agricultural\atk-crankspur-rooster-creature-pet-t1-arcane-engineering-slot11-atk-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\rural_agricultural\atk-crankspur-rooster-creature-pet-t1-arcane-engineering-slot11-atk-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\rural_agricultural\atk-crankspur-rooster-creature-pet-t1-arcane-engineering-slot11-atk-walk-4dof-1024.manifest.json

Created then removed as failed output cleanup:

- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\rural_agricultural\def-chaffplate-goat-creature-pet-t1-arcane-engineering-slot11-def-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\rural_agricultural\def-chaffplate-goat-creature-pet-t1-arcane-engineering-slot11-def-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\rural_agricultural\def-chaffplate-goat-creature-pet-t1-arcane-engineering-slot11-def-walk-4dof-1024.manifest.json

Created then removed as temporary cleanup:

- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\tmp-ae-08

Read or inspected:

- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\AGENTS.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-creature-spritesheets\overview.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-creature-spritesheets\asset-contract.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-creature-spritesheets\decisions.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-creature-spritesheets\automation-plan.md
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\CREATURE_WALK_SPRITESHEET_USAGE.md
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\T1_CREATURE_WALK_SPRITESHEET_HOWTO.md
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\art\repack_creature_walk_sheet.py
- C:\Users\yrred\.codex\generated_images\019e1b4e-c590-7ac1-afb4-dd146df41aaa\ig_0b6be89314cf0380016a02e609c0148190bca4ec3de716fbc0.png
- C:\Users\yrred\.codex\generated_images\019e1b4e-c590-7ac1-afb4-dd146df41aaa\ig_0b6be89314cf0380016a02e7e70e188190b3d7f0ed55d42616.png

## Checks Run

Rooster:

- Generated a 4x4 walk sheet from the source portrait with magenta #FF00FF matte.
- Ran chroma removal with remove_chroma_key.py using #FF00FF, soft matte, edge contract, and despill.
- Ran tools\art\repack_creature_walk_sheet.py.
- Ran mechanical QA: 1024x1024, RGBA, alpha extrema include 0 and 255, corner alpha all 0, all 16 cells populated, .png.meta exists, spriteMode: 2, alphaIsTransparency: 1, 16 unique slice names, .manifest.json exists.
- Ran finishing QA for obvious magenta/green edge pixels; final sample count was zero.
- Visual sniff test: usable down/left/right/up rows; no visible matte or outline artifact detected.

Goat:

- Generated a 4x4 walk sheet from the source portrait with magenta matte requested.
- Visual precheck showed the generated sheet had usable creature poses but the matte was visibly gradient/non-uniform.
- Ran chroma removal and repack attempt.
- Repack output failed visual QA: frames were severely undersized because background residue inflated component bounds.
- Invalid final goat .png, .png.meta, and .manifest.json were removed.

## Finishing Pass Performed

- Rooster: yes. Chroma removal, edge contract, despill, final alpha-noise cleanup at alpha <= 8, and magenta/green edge artifact check.
- Goat: attempted, but failed due to non-flat generated matte; final output was rejected and removed.
- Mouse: not attempted because the package stopped on goat failure.

## Cleanup Performed

- Removed failed goat final project outputs created during this run.
- Removed temporary cleaned-sheet folder C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\tmp-ae-08.
- Preserved generated-image provenance under C:\Users\yrred\.codex\generated_images\.
- Released singleton lock after writing this report.

## Blockers

- def-chaffplate-goat needs regeneration with a truly flat #FF00FF matte or a more robust background-removal/repack strategy. The current generated source violated the flat-matte requirement with a visible magenta gradient.

## Risks

- AE-08 is now partially produced: rooster assets exist and passed QA, but the triad is not complete and the queue remains pending.
- A future run should decide whether to reuse the passed rooster asset or regenerate the whole triad for consistency.
- The prompt may need stronger wording to forbid radial lighting or tonal variation in the chroma matte.

## Memory-Worthy Notes

- AE-08 attempted on 2026-05-12 and blocked on def-chaffplate-goat due to non-flat magenta matte causing repack scale failure.
- atk-crankspur-rooster final walk sheet passed QA and remains in the rural agricultural folder.

## Do-Not-Promote Notes

- Do not mark AE-08 complete.
- Do not promote goat output as valid; failed final assets were removed.
- Do not treat the generated goat source image as accepted art.

## Follow-Up Recommendations

- Rerun AE-08 with def-chaffplate-goat first, using stricter flat-matte wording: no radial lighting, no vignette, no hue variation, no shaded background.
- Consider adding a pre-repack matte-uniformity check so gradient mattes fail before project outputs are written.
- If future automation sees the rooster final assets, run QA and reuse only if still passing.

## Lock Contents Before Release

~~~~json
{
  "timestamp": "2026-05-12T08:32:27.8030879Z",
  "automation_id": "twb-sprite-sheet-triad-runner",
  "intended_chunk": "AE-08 arcane-engineering/rural_agricultural",
  "cwd": "C:\\Users\\yrred\\Documents\\New project 2",
  "note": "Fresh lock acquired before queue selection."
}

~~~~
