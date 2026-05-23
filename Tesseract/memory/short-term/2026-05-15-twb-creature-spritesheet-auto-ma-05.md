# TWB Creature Sprite-Sheet Automation - MA-05

- Task: Process exactly one pending TWB creature family triad package for The World Beneath.
- Lock status: acquired normally before queue selection, heartbeated after selection, after each creature, and before report write; released after this report and memory update.
- Stale-lock recovery: none.
- Chunk processed or skipped reason: processed `MA-05` / `magic` / `industrial`, the next pending row in `CHUNK_QUEUE.md`.
- Result: `QA Passed`; queue row updated after all three creatures passed mechanical and visual QA.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\atk-sparkgnaw-tenrec-creature-pet-t1-magic-iota-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\atk-sparkgnaw-tenrec-creature-pet-t1-magic-iota-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\atk-sparkgnaw-tenrec-creature-pet-t1-magic-iota-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\def-boilerback-roach-creature-pet-t1-magic-iota-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\def-boilerback-roach-creature-pet-t1-magic-iota-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\def-boilerback-roach-creature-pet-t1-magic-iota-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\util-chalkwing-moth-creature-pet-t1-magic-iota-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\util-chalkwing-moth-creature-pet-t1-magic-iota-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\magic\industrial\util-chalkwing-moth-creature-pet-t1-magic-iota-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\MA-05_working_provenance\atk-sparkgnaw-tenrec-generated-clean.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\MA-05_working_provenance\def-boilerback-roach-generated-clean.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\MA-05_working_provenance\util-chalkwing-moth-generated-clean.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\MA-05_working_provenance\ma-05-visual-qa-preview-black-light.png`
- Generated originals retained under `C:\Users\yrred\.codex\generated_images\019e2c00-c5b2-7191-8c74-f507e2298c11\`.

## Checks Run

- Confirmed the queue target after lock acquisition: `MA-05` / `magic` / `industrial`.
- Inspected source card art and creature prompts for Sparkgnaw Tenrec, Boilerback Roach, and Chalkwing Moth.
- Generated one 4x4 source sheet per creature with magenta `#FF00FF` matte prompt.
- Ran chroma-key alpha extraction with `remove_chroma_key.py` on each generated source before repacking.
- Ran `tools\art\repack_creature_walk_sheet.py` for each creature.
- Verified each final PNG is `1024x1024`, `RGBA`, alpha extrema include `0` and `255`, all corner alpha values are `0`, and all `16` cells are populated.
- Verified each `.png.meta` exists, has `spriteMode: 2`, `alphaIsTransparency: 1`, and `16` slice names.
- Verified each `.manifest.json` exists and records row order `down`, `left`, `right`, `up`.
- Ran edge-fringe sniff after finishing: `0` magenta, `0` green, and `0` lime suspect edge pixels on all three final sheets.
- Visual QA preview checked on dark and light backgrounds.

## Finishing Pass Performed

- `atk-sparkgnaw-tenrec`: pre-repack chroma extraction, boundary matte/fringe cleanup, low-alpha snap, and one lime-ish edge bead recolored to the creature's cyan spark accent.
- `def-boilerback-roach`: pre-repack chroma extraction, boundary matte/fringe cleanup, low-alpha snap.
- `util-chalkwing-moth`: pre-repack chroma extraction, boundary matte/fringe cleanup, low-alpha snap.

## Cleanup Performed

- No throwaway logs or temporary dev files were left.
- Working provenance files were kept because manifests reference the cleaned generated sheets and the visual QA preview is useful evidence for this run.
- Singleton lock was released after report and memory update.

## Blockers

- None.

## Risks

- Motion quality has been visually checked at the sheet level but not in Unity animation playback.
- The built-in image generator produced slightly gradient magenta backgrounds, so strict chroma extraction was required before repack.

## Memory-Worthy Notes

- `MA-05` / `magic` / `industrial` is complete and queue-updated as `QA Passed` with `atk-sparkgnaw-tenrec`, `def-boilerback-roach`, and `util-chalkwing-moth`.
- For magenta-matte sprite sheets, pre-repack chroma extraction produces cleaner final edges than relying only on the repacker's edge-background removal.
- Next pending queue target is `MA-06` / `magic` / `marine`.

## Do-Not-Promote Notes

- Do not promote implementation minutiae such as exact generated image IDs unless provenance lookup is needed.

## Follow-Up Recommendations

- Continue with `MA-06` / `magic` / `marine` on the next run.
- Keep using pre-repack chroma extraction plus visual dark/light preview for generated sheets with gradient magenta matte.
