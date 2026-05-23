# TWB Creature Sprite Sheet Automation - MN-02

- Task: TWB Sprite Sheet Single Runner, one family triad package.
- Automation ID: twb-sprite-sheet-triad-runner
- Run time: 2026-05-16 09:01:11 -05:00
- Launch workspace: C:\Users\yrred\Desktop\Obsidian\Tesseract

## Lock Status

- Singleton lock acquired with exclusive create-new semantics before queue selection.
- Lock file: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json
- Heartbeat refreshed after acquisition, chunk selection, each creature, and before final report/cleanup.
- Stale-lock recovery: none; no stale lock was present.
- Lock release: scheduled after this report and cleanup.

## Chunk Processed

- Chunk: MN-02
- Affinity: mind
- Biome: desert
- Status before run: Pending
- Status after run: QA Passed
- Creatures processed: `atk-glassfang-sidewinder`, `def-sunshell-tortoise`, `util-hushcall-sandgrouse`
- Queue update: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md line for MN-02 updated only after all three passed QA.

## Result

Completed exactly one triad package. Generated one full #FF00FF-matte 4x4 sheet per creature with built-in image generation, copied raw outputs into run scratch for processing, removed magenta matte, repacked with the project helper, ran finishing passes, visually inspected dark/light composites, and accepted final Unity-ready PNG/.meta/.manifest siblings beside the source card art.

## Files Touched

- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\atk-glassfang-sidewinder-creature-pet-t1-mind-gamma-atk-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\atk-glassfang-sidewinder-creature-pet-t1-mind-gamma-atk-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\atk-glassfang-sidewinder-creature-pet-t1-mind-gamma-atk-walk-4dof-1024.manifest.json
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\def-sunshell-tortoise-creature-pet-t1-mind-gamma-def-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\def-sunshell-tortoise-creature-pet-t1-mind-gamma-def-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\def-sunshell-tortoise-creature-pet-t1-mind-gamma-def-walk-4dof-1024.manifest.json
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\util-hushcall-sandgrouse-creature-pet-t1-mind-gamma-util-walk-4dof-1024.png
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\util-hushcall-sandgrouse-creature-pet-t1-mind-gamma-util-walk-4dof-1024.png.meta
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\mind\desert\util-hushcall-sandgrouse-creature-pet-t1-mind-gamma-util-walk-4dof-1024.manifest.json
- C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md
- C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-creature-spritesheet-auto-mn-02.md
- C:\Users\yrred\.codex\automations\twb-sprite-sheet-triad-runner\memory.md

## Checks Run

- Project helper: `tools\art\repack_creature_walk_sheet.py` for all three creatures.
- Chroma removal helper: `remove_chroma_key.py` with `--key-color #FF00FF`, soft matte, and despill.
- Aggregate mechanical QA passed for all three: PNG exists, 1024x1024, RGBA, alpha extrema include 0 and 255, corner alpha values are 0, all 16 cells populated, `.png.meta` exists, `spriteMode: 2`, `alphaIsTransparency: 1`, 16 slice names, `.manifest.json` exists, row order `down,left,right,up`, 4 frames per direction.
- Aggregate edge artifact QA passed: strict magenta edge pixels 0 and strict lime/green edge pixels 0 on all three final PNGs.
- Visual QA performed on dark and light composites for all three final sheets; row order and silhouettes were usable.

## Finishing Pass Performed

- `atk-glassfang-sidewinder`: removed 53 low-alpha chroma edge crumbs after matte removal.
- `def-sunshell-tortoise`: removed 43 low-alpha chroma edge crumbs after matte removal.
- `util-hushcall-sandgrouse`: removed 39 low-alpha chroma edge crumbs after matte removal.
- Manifests include a `postprocess.finishing_pass` note for the cleanup.

## Cleanup Performed

- Removed run scratch folder: C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\_automation_scratch\MN-02-20260516T1340Z
- Temporary raw copies, dechromed intermediates, and dark/light preview composites from this run were removed.
- Raw generated-image provenance preserved under: C:\Users\yrred\.codex\generated_images\019e3102-e096-7e82-9832-f6166a7e60dc

## Blockers

- None.

## Risks

- The `atk-glassfang-sidewinder` source card art is visually a robotic quadruped rather than a snake/sidewinder. The run followed the stronger rule that source card art is the identity lock, and the generated walk sheet preserves the visible approved source design.
- The sandgrouse raw generation was landscape-sized, not square; the component-based repacker normalized it successfully to the contract.

## Memory-Worthy Notes

- MN-02 / mind / desert is complete and marked QA Passed.
- Final creatures: `atk-glassfang-sidewinder`, `def-sunshell-tortoise`, `util-hushcall-sandgrouse`.
- Next expected queue target: MN-03 / mind / freshwater.

## Do-Not-Promote Notes

- Do not promote the Glassfang name/art mismatch as a durable design issue without a curator review; it may be accepted source-card lineage.
- Do not promote raw generation paths beyond provenance unless needed for audit.

## Follow-Up Recommendations

- Continue next run with exactly one package: MN-03 / mind / freshwater, if still Pending.
- Keep explicit row-order prompting for birds and other lightweight utility creatures.
