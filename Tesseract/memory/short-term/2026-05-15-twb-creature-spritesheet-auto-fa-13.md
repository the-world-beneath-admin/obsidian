# TWB Creature Spritesheet Automation - FA-13

- task: TWB Sprite Sheet Single Runner
- automation_id: twb-sprite-sheet-triad-runner
- run_time: 2026-05-15 04:29:02 -05:00 / 2026-05-15T09:29:02Z UTC
- lock_status: acquired with create-new semantics, refreshed after selection and after each completed creature, released after report and memory update
- stale_lock_recovery: none
- chunk_processed: FA-13 / faith / urban_residential
- result: QA Passed; CHUNK_QUEUE.md updated after all three creatures passed

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\atk-dawnbeak-creature-pet-t1-faith-slot13-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\atk-dawnbeak-creature-pet-t1-faith-slot13-atk-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\atk-dawnbeak-creature-pet-t1-faith-slot13-atk-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\def-gableguard-creature-pet-t1-faith-slot13-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\def-gableguard-creature-pet-t1-faith-slot13-def-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\def-gableguard-creature-pet-t1-faith-slot13-def-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\util-murmurdove-creature-pet-t1-faith-slot13-util-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\util-murmurdove-creature-pet-t1-faith-slot13-util-walk-4dof-1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\faith\urban_residential\util-murmurdove-creature-pet-t1-faith-slot13-util-walk-4dof-1024.manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\fa-13-atk-dawnbeak-raw-magenta.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\fa-13-atk-dawnbeak-cleaned-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\fa-13-def-gableguard-raw-magenta.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\fa-13-def-gableguard-cleaned-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\fa-13-util-murmurdove-raw-magenta.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\fa-13-util-murmurdove-cleaned-transparent.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- Raw generated provenance retained under `C:\Users\yrred\.codex\generated_images\019e2ae6-d58b-7df2-adbd-9b871e3f8f5f\`.

## Checks Run

- Source card art inspected for Dawnbeak, Gableguard, and Murmurdove.
- One generated 4x4 sheet per creature using flat magenta `#FF00FF` matte.
- Chroma removal via installed imagegen `remove_chroma_key.py` helper.
- Project repacker `tools\art\repack_creature_walk_sheet.py` run once per creature.
- Per-creature visual review after final repack.
- Triad-wide mechanical QA: `1024x1024`, `RGBA`, alpha extrema include `0` and `255`, corner alpha `0`, all 16 cells populated, `.png.meta` exists, `spriteMode: 2`, `alphaIsTransparency: 1`, 16 slice names, `.manifest.json` exists, manifest generated source exists, row order `down/left/right/up`, 16 placements.
- Finishing-pass chroma sniff: zero low-alpha magenta samples, zero chroma-lime edge samples, zero nonzero RGB in fully transparent pixels.

## Finishing Pass Performed

- Removed magenta matte with soft matte/despill.
- Applied conservative low-alpha cleanup to remove residual 1-2 px matte specks and transparent RGB residue.
- Gableguard and Murmurdove retained intentional source-like green/gold ornament/roof accents; sniff only rejected low-alpha chroma-lime residue, not opaque design colors.

## Cleanup Performed

- No throwaway scripts, previews, or logs were created.
- Raw magenta sheets and cleaned generated sheets were retained in the queue folder as production evidence; cleaned sheets are referenced by manifests.
- Singleton lock removed after report and automation memory update.

## Blockers

- None.

## Risks

- Mechanical and visual sprite-sheet QA passed, but no Unity Editor import or runtime animation smoke test was run in this automation.
- Decorative tag marks on generated birds are tiny sprite-like glyphs inherited from the charm/tag concept, not UI labels; they looked acceptable in visual review.

## Memory-Worthy Notes

- FA-13 / faith / urban_residential is complete and queue-updated as `QA Passed` with `atk-dawnbeak`, `def-gableguard`, and `util-murmurdove` walk-4dof-1024 PNGs plus `.meta` and `.manifest.json` beside source art.
- Faith affinity is complete through FA-13. Next pending queue target is MA-01 / magic / boreal_forest.
- Current generation folder: `C:\Users\yrred\.codex\generated_images\019e2ae6-d58b-7df2-adbd-9b871e3f8f5f`.

## Do-Not-Promote Notes

- Do not promote this as Unity runtime wiring or live animation validation.
- Do not delete retained raw/cleaned evidence unless the asset contract changes.

## Follow-Up Recommendations

- Next automation run should process exactly one pending triad: MA-01 / magic / boreal_forest.
- Consider a later Unity import spot-check for several completed sheets after the art batch advances.
