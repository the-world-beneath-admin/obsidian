# TWB Creature Spritesheet Automation - FA-08

- task: TWB Sprite Sheet Single Runner
- run timestamp local: 2026-05-14T23:27:00-05:00
- run timestamp UTC: 2026-05-15T04:27:00Z
- lock status: acquired before queue selection; heartbeat refreshed after selection, after each creature, and before report write
- stale-lock recovery: none
- chunk processed: FA-08 / faith / rural_agricultural
- skipped reason: none
- result: QA Passed; queue updated after all three creatures passed mechanical QA, finishing pass, and visual inspection

## Creatures Completed

- atk-spurbeak: first generation rejected because the down/front row read too profile-heavy; regenerated with stricter row-facing prompt, chroma-prepared with #FF00FF removal/despill, repacked, finished, visual QA passed
- def-woolward: generated, chroma-prepared with #FF00FF removal/despill, repacked, finished, visual QA passed
- util-wickmoth: first generation rejected because the magenta matte had glow/gradient; second generation used for rows after border-connected matte was normalized to flat #FF00FF, chroma-prepared, repacked, finished, visual QA passed

## Files Touched

- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\FA-08-atk-spurbeak-generated-transparent.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\FA-08-def-woolward-generated-transparent.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\FA-08-util-wickmoth-generated-transparent.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\atk-spurbeak-creature-pet-t1-faith-alpha-atk-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\atk-spurbeak-creature-pet-t1-faith-alpha-atk-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\atk-spurbeak-creature-pet-t1-faith-alpha-atk-walk-4dof-1024.manifest.json
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\def-woolward-creature-pet-t1-faith-alpha-def-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\def-woolward-creature-pet-t1-faith-alpha-def-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\def-woolward-creature-pet-t1-faith-alpha-def-walk-4dof-1024.manifest.json
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\util-wickmoth-creature-pet-t1-faith-alpha-util-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\util-wickmoth-creature-pet-t1-faith-alpha-util-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\rural_agricultural\util-wickmoth-creature-pet-t1-faith-alpha-util-walk-4dof-1024.manifest.json
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-creature-spritesheet-auto-fa-08.md

## Generated Provenance

- rejected raw Spurbeak: C:\Users\yrred\.codex\generated_images\019e29cf-0fb1-7ea1-94a7-37f484e22a08\ig_055aca3313ebefa8016a069c11487c8199b1cc9a17164c947e.png
- accepted raw Spurbeak: C:\Users\yrred\.codex\generated_images\019e29cf-0fb1-7ea1-94a7-37f484e22a08\ig_055aca3313ebefa8016a069ce9828c81999f270e4347f22271.png
- accepted raw Woolward: C:\Users\yrred\.codex\generated_images\019e29cf-0fb1-7ea1-94a7-37f484e22a08\ig_055aca3313ebefa8016a069db406948199a3e035aa2b21429e.png
- rejected raw Wickmoth: C:\Users\yrred\.codex\generated_images\019e29cf-0fb1-7ea1-94a7-37f484e22a08\ig_055aca3313ebefa8016a069eb200b881998e51434effd79024.png
- accepted raw Wickmoth, after local matte normalization: C:\Users\yrred\.codex\generated_images\019e29cf-0fb1-7ea1-94a7-37f484e22a08\ig_055aca3313ebefa8016a069f1e5ccc8199a1f016b2928de2e7.png

## Checks Run

- source card art inspected for all three creatures
- generated sheet visual QA for 4x4 layout and down/left/right/up row usability
- remove_chroma_key.py with key color #FF00FF, soft matte, edge-contract 1, and despill before repack
- Wickmoth-only border-connected matte normalization to flat #FF00FF before chroma removal because raw image generation returned a pink gradient
- tools/art/repack_creature_walk_sheet.py for each accepted sheet
- finishing pass removed low-alpha edge crumbs and visible key-color pixels after repack
- aggregate mechanical QA confirmed 1024x1024 RGBA, alpha extrema 0/255, transparent corners, all 16 cells populated, .png.meta exists, spriteMode: 2, alphaIsTransparency: 1, 16 slice names, .manifest.json exists, row order down/left/right/up, 16 placements
- edge artifact sniff found 0 key-magenta, 0 green/lime, and 0 low-alpha visible edge pixels after final finishing pass for all three final sheets
- close visual inspection found no visible matte, outline halo, or cropping artifacts on the accepted final sheets

## Finishing Pass Performed

- yes; each accepted sheet went through #FF00FF matte removal/despill before repack and low-alpha/key-color cleanup after repack
- Spurbeak final finishing cleanup removed 16,878 pixels: 143 key-color pixels and 16,735 low-alpha crumbs
- Woolward final finishing cleanup removed 13,642 pixels: 126 key-color pixels and 13,516 low-alpha crumbs
- Wickmoth final finishing cleanup removed 20,931 pixels: 137 key-color pixels and 20,794 low-alpha crumbs

## Cleanup Performed

- removed temporary file: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\FA-08-util-wickmoth-generated-flat-magenta.tmp.png
- no scratch scripts, previews, or throwaway logs were left behind
- prepared transparent generated sheets were retained in the queue folder as useful provenance referenced by manifests
- raw generated images under C:\Users\yrred\.codex\generated_images were left in place as provenance, including rejected attempts
- singleton lock scheduled for deletion immediately after report and automation-memory update

## Blockers

- none

## Risks

- mechanical QA cannot prove in-engine motion feel; Unity/runtime animation review remains the stronger confidence gate
- Wickmoth raw generation repeatedly preferred a pink gradient matte; the final accepted asset is clean, but future flying/winged Faith utility prompts may need the same matte-normalization guard

## Memory-Worthy Notes

- FA-08 / faith / rural_agricultural is complete and marked QA Passed.
- Completed creatures: atk-spurbeak, def-woolward, util-wickmoth.
- Spurbeak required one regeneration because the first down/front row read too side-facing.
- Wickmoth required matte normalization because image generation produced magenta gradient backgrounds even under flat #FF00FF instructions.
- Next pending queue target is FA-09 / faith / temperate_forest.

## Do-Not-Promote Notes

- Do not promote the rejected first Spurbeak raw generation as accepted art.
- Do not treat the raw Wickmoth generated images as direct final/repack sources without the prepared transparent cleanup path.
- Do not treat generated-source provenance files as runtime Unity assets.
- No memory/wiki files were edited by this worker.

## Follow-Up Recommendations

- Next automation run should process exactly FA-09 / faith / temperate_forest if still pending.
- Keep using #FF00FF prepared transparent source plus despill before repack to avoid matte halos.
- For winged/glowy Faith creatures, explicitly forbid glow/gradient matte and be prepared to normalize border-connected magenta before chroma removal.
