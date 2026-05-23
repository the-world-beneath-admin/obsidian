# TWB Creature Sprite Sheet Automation - CU-02

- task: TWB Sprite Sheet Single Runner
- automation_id: twb-sprite-sheet-triad-runner
- run_time: 2026-05-13T16:49:22.2911770Z
- lock_status: acquired normally, updated with intended chunk `CU-02`, released after report/memory update
- chunk_processed: `CU-02` / `cunning` / `desert` / Saltglass Scavengers
- result: `QA Passed`; queue updated after all three creatures passed mechanical QA, finishing pass, and visual inspection

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\atk-glassfang-roadrunner-creature-pet-t1-cunning-delta-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\atk-glassfang-roadrunner-creature-pet-t1-cunning-delta-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\atk-glassfang-roadrunner-creature-pet-t1-cunning-delta-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\def-shardback-horned-lizard-creature-pet-t1-cunning-delta-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\def-shardback-horned-lizard-creature-pet-t1-cunning-delta-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\def-shardback-horned-lizard-creature-pet-t1-cunning-delta-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\util-heatshiver-jerboa-creature-pet-t1-cunning-delta-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\util-heatshiver-jerboa-creature-pet-t1-cunning-delta-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\cunning\desert\util-heatshiver-jerboa-creature-pet-t1-cunning-delta-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-02\atk-glassfang-roadrunner-generated-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-02\def-shardback-horned-lizard-generated-cleaned.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\generated-cleaned\CU-02\util-heatshiver-jerboa-generated-cleaned.png`
- raw generated image provenance retained under `C:\Users\yrred\.codex\generated_images\019e2225-4eef-7521-9de0-62e575c6c99a\`
- this report: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-creature-spritesheet-auto-cu-02.md`

## Checks Run

- Loaded source card art as identity locks for Glassfang Roadrunner, Shardback Horned Lizard, and Heatshiver Jerboa.
- Generated one full 4x4 walk sheet per creature with magenta `#FF00FF` matte only.
- Ran `remove_chroma_key.py` with auto-key border, soft matte, edge-contract `1`, and despill.
- Ran `repack_creature_walk_sheet.py` for each creature to create final PNG, `.png.meta`, and `.manifest.json` beside source card art.
- Ran finishing cleanup to remove low-alpha magenta/green/white/dark matte crumbs after repack.
- Consolidated QA passed for each final PNG: `1024x1024`, `RGBA`, alpha extrema include `0` and `255`, all corner alpha values `0`, all 16 cells populated, no tight/cropped cells, `.png.meta` exists, `spriteMode: 2`, `alphaIsTransparency: 1`, 16 slice names, and manifest exists.
- Edge QA passed with `0` low-alpha magenta-like and `0` low-alpha green-like edge pixels on all three final sheets.
- Visual QA confirmed usable row order as down/front, left, right, up/back and no visible matte or outline artifacts.

## Finishing Pass Performed

Yes. Each creature was cleaned with chroma removal/despill before repack, then a final low-alpha edge cleanup removed residual matte crumbs. The first Roadrunner repack exposed a visible magenta fringe, so it was rejected and rerun through the stricter cleanup path before acceptance.

## Cleanup Performed

No throwaway previews or logs were left. The three cleaned generated sheets under `generated-cleaned\CU-02\` were retained deliberately because the final manifests reference them as the repack input and they preserve the exact chroma-cleaned generation evidence. Raw generated images in `.codex\generated_images\` were also retained as provenance.

## Blockers

None.

## Risks

- Motion quality is mechanically and visually usable but not a Unity runtime animation test.
- The retained cleaned generated sheets are extra provenance files; keep them unless the manifest provenance approach is later changed.

## Memory-Worthy Notes

- `CU-02` / `cunning` / `desert` is complete and marked `QA Passed`.
- Completed creatures: `atk-glassfang-roadrunner`, `def-shardback-horned-lizard`, and `util-heatshiver-jerboa`.
- The magenta matte path worked, but final acceptance required both helper despill and a post-repack low-alpha edge cleanup to eliminate chroma crumbs.
- Next pending queue target is `CU-03` / `cunning` / `freshwater`.

## Do-Not-Promote Notes

- Do not promote the raw/cleaned generated image paths as canonical runtime assets; only the final `*-walk-4dof-1024.png` files beside source card art are runtime-facing.
- Do not infer that every future sheet can skip visual QA because CU-02 passed mechanically.

## Follow-Up Recommendations

- Next automation run should process exactly one triad: `CU-03` / `cunning` / `freshwater`, unless the queue changes before then.
- Continue using magenta matte plus explicit low-alpha edge cleanup; it caught artifacts that the basic repack path left behind.
