# TWB Creature Sprite Sheet Automation - AE-11 Complete

Run time: 2026-05-12T08:01:08.3030602-05:00
Automation ID: `twb-sprite-sheet-triad-runner`

## Task

Process exactly one pending family triad package for **Main game / The World Beneath** creature walk sprite sheets.

Selected chunk: `AE-11` / `arcane-engineering` / `tundra`

Creatures:

- `atk-caliperbite-lemming`
- `def-snowplate-ptarmigan`
- `util-beaconpin-stoat`

## Lock Status

- Singleton lock acquired with exclusive create-new semantics before queue selection.
- No fresh competing lock was present.
- Lock updated after selection with intended chunk `AE-11`.
- Lock was held through generation, QA, queue update, report writing, and cleanup.

## Result

`AE-11` completed and `CHUNK_QUEUE.md` was updated to `QA Passed`.

Final assets were generated beside the source card art:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\tundra\atk-caliperbite-lemming-creature-pet-t1-arcane-engineering-iota-atk-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\tundra\def-snowplate-ptarmigan-creature-pet-t1-arcane-engineering-iota-def-walk-4dof-1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\.md\T1_Creature_Art_Prompt_System\affinities\arcane-engineering\tundra\util-beaconpin-stoat-creature-pet-t1-arcane-engineering-iota-util-walk-4dof-1024.png`

Each final PNG has a sibling `.png.meta` and `.manifest.json`.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\AE-11-alpha-sources\`
- Final PNG, `.png.meta`, and `.manifest.json` files for all three AE-11 creatures.

Generated-image provenance preserved:

- `C:\Users\yrred\.codex\generated_images\019e1c2f-c118-7e63-aa91-5efc58392a65\ig_066150ae18353580016a031f5baa248194a5fcf1ac5253caa2.png`
- `C:\Users\yrred\.codex\generated_images\019e1c2f-c118-7e63-aa91-5efc58392a65\ig_066150ae18353580016a0320650c7c8194b941dadbae056e5f.png`
- `C:\Users\yrred\.codex\generated_images\019e1c2f-c118-7e63-aa91-5efc58392a65\ig_066150ae18353580016a0321ddf358819481ae0e8230ddacd7.png`

Rejected generated-image provenance preserved:

- `C:\Users\yrred\.codex\generated_images\019e1c2f-c118-7e63-aa91-5efc58392a65\ig_066150ae18353580016a03210ef5a88194afd0b763c676d271.png`

## Checks Run

- Read required sprite-sheet memory lane and project pipeline docs.
- Selected only the next pending queue item, `AE-11`.
- Generated one creature at a time using source card art as the identity lock.
- Used flat magenta `#FF00FF` as the temporary chroma matte.
- Rejected the first stoat generation because its top row read too much like a right-facing pose instead of a down/front row.
- Corrected the lemming generated row order by swapping the left/right side rows before matte removal.
- Removed chroma matte with `remove_chroma_key.py`, then applied alpha clamp and transparent-RGB edge bleed before repack.
- Repacked each accepted alpha-bleed sheet with `tools\art\repack_creature_walk_sheet.py`.
- Mechanical QA confirmed for all three final sheets:
  - `1024x1024`
  - `RGBA`
  - alpha extrema include `0` and `255`
  - all corner alpha values are `0`
  - all `16` cells populated
  - `.png.meta` exists
  - `spriteMode: 2`
  - `alphaIsTransparency: 1`
  - `16` slice names
  - `.manifest.json` exists and loads
- Visual QA confirmed usable row order as down/front, left, right, up/back.
- Light and dark background contact-sheet inspection showed no visible magenta, green/lime, checkerboard, or cutout matte outline artifacts.

## Finishing Pass Performed

- `atk-caliperbite-lemming`: row-order correction, chroma removal, edge contraction/despill, alpha-noise clamp, alpha edge-bleed finish, repack, and visual QA.
- `def-snowplate-ptarmigan`: chroma removal, edge contraction/despill, alpha-noise clamp, alpha edge-bleed finish, repack, and visual QA.
- `util-beaconpin-stoat`: first generation rejected for ambiguous front row; second generation accepted, chroma removal, edge contraction/despill, alpha-noise clamp, alpha edge-bleed finish, repack, and visual QA.

## Cleanup Performed

- Removed temporary visual QA contact-sheet folder `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\tmp-ae-11`.
- Preserved generated-image provenance under `C:\Users\yrred\.codex\generated_images\019e1c2f-c118-7e63-aa91-5efc58392a65\`.
- Preserved accepted alpha-source and alpha-bleed inputs under `AE-11-alpha-sources` because final manifests reference the accepted bleed inputs.
- No Unity runtime code was modified.

## Blockers

None.

## Risks

- Mechanical QA does not prove in-engine animation feel; Unity import/motion preview was not run.
- Stoat side rows include long tail and small disconnected accessory/whisker details; they passed visual QA, but in-engine scale may make tiny details flicker.
- Lemming side rows required row-order correction before acceptance; future runs should keep watching for generator left/right swaps.

## Memory-Worthy Notes

- `AE-11` / `arcane-engineering` / `tundra` is now complete and queue-marked `QA Passed`.
- The accepted triad is `atk-caliperbite-lemming`, `def-snowplate-ptarmigan`, and `util-beaconpin-stoat`.
- The first stoat generation was rejected because the front row was directionally ambiguous.
- The magenta matte plus alpha edge-bleed finishing path remained viable for tundra creatures with pale fur/feathers.

## Do-Not-Promote Notes

- Do not promote temporary contact-sheet previews; they were removed.
- Do not infer Unity runtime animation quality from mechanical sprite-sheet QA alone.
- Do not promote the rejected stoat sheet as an accepted asset.

## Follow-Up Recommendations

- Next automation run should start at `AE-12` / `arcane-engineering` / `urban_commercial`.
- Continue checking row direction manually before repack, especially top-row down/front and side-row left/right order.
