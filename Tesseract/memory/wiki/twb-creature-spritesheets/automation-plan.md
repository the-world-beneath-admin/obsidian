# TWB Creature Sprite Sheet Automation Plan

## Status

Paused / complete - created 2026-05-12, activated 2026-05-12, paused 2026-05-17 after the queue completed.

## Purpose

The recurring Codex automation processed Tier 1 creature sprite-sheet packages one triad at a time until the full Tier 1 set was complete.

## Cadence

- User request during production: run once per hour.
- Decision - The automation is now paused because all `117` triad chunks are marked `QA Passed`.

## Automation Workspace

The Codex automation should run from a single workspace only:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract
```

Do not configure multiple `cwds` for this automation. Multiple workspaces can fan out into duplicate chat runs that process the same queue item.

The Tesseract vault is intentionally the launch project now that the user saved it as a visible Codex project. The automation may read and write Unity art-pipeline files by absolute path, but it should not launch from Unity folders, the main game project, or the orchestration workspace.

## Singleton Lock

Before selecting a queue item or generating assets, the automation must acquire this lock:

```text
C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json
```

Rules:

- Create the lock with exclusive create/new-file semantics.
- If the lock exists and is less than 90 minutes old, write a skipped-run report and stop without modifying `CHUNK_QUEUE.md`.
- If the lock exists and is 90 minutes old or older, treat it as stale/orphaned, report that, archive or replace it, and continue.
- Refresh the lock heartbeat after acquiring it, after selecting a chunk, after each creature completes, and before writing the final report so long but healthy runs are not mistaken for stale.
- Release/delete the lock only after the run has written its report and finished cleanup.
- Do not process a chunk if the lock could not be acquired.

## Work Unit

One run should process exactly one family triad package:

- `3` creatures maximum per run
- `1` folder / family triad maximum per run
- each triad has the same affinity and biome
- each triad usually contains one `atk`, one `def`, and one `util`

## Run Behavior

Each run should:

1. Read the current sprite-sheet memory lane and source pipeline docs.
2. Acquire the singleton lock.
3. Inspect `CHUNK_QUEUE.md`.
4. Find the next `Pending` family triad.
5. Process exactly one triad package.
6. Generate/repack/QA one creature at a time.
7. Use flat magenta `#FF00FF` only for any temporary solid/chroma matte; do not use lime or green matte backgrounds.
8. Run a finishing pass before acceptance to remove matte/chroma spill, cutout halos, and 1-2 px outline artifacts.
9. Update `CHUNK_QUEUE.md` only after all three creatures in a triad pass QA, including the finishing-pass visual check.
10. Write a short-term report under `memory/short-term/`.
11. Release the singleton lock after the report and cleanup are complete.
12. Stop if the queue is complete.
13. Stop and report a blocker if any creature fails generation, finishing pass, repacking, visual QA, or mechanical QA.

## Required Safety Rails

- Do not run broad cleanup or revert operations.
- Do not modify Unity code/runtime systems.
- Do not delete source art, generated-image provenance, raw evidence, reports, or another worker's work.
- Do not skip visual QA.
- Do not skip the finishing pass.
- Do not accept visible green, lime, magenta, white, dark, or colored fringe around the sprite.
- Do not use lime/green matte backgrounds during generation or cleanup.
- Do not mark a triad complete unless all three creatures pass the asset contract.
- Do not continue past one triad package in the same run.
- Do not process if another live run holds the singleton lock.

## Final Production State

- `CHUNK_QUEUE.md` contains `117` triad chunks.
- All `117` triad chunks are marked `QA Passed`.
- `RO-13` / `robotics` / `urban_residential` was the final completed triad.
- `CHUNK_QUEUE.md` has no remaining `Pending` rows.
- Codex automation id `twb-sprite-sheet-triad-runner` / `TWB Sprite Sheet Single Runner` is paused.
- Optional follow-up: run Unity import/playback spot checks for the final robotics sheets.
- 2026-05-14: A stale/orphaned `CY-08` lock blocked the runner for roughly two hours under the older 3-hour threshold. Bob archived and removed the orphan lock, then changed the stale threshold to 90 minutes with heartbeat refresh requirements.

## Output

Each run writes a report to:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\
```

Report filename pattern:

```text
YYYY-MM-DD-twb-creature-spritesheet-<chunk-id>.md
```

## Memory Items

- Decision - Recurring sprite-sheet production should process exactly one family triad package per hourly run.
- Decision - The recurring automation should run after the first sprite-sheet result was approved.
- Decision - Use hourly standalone Codex automation for production work.
- Decision - The automation should use only one configured workspace, `C:\Users\yrred\Desktop\Obsidian\Tesseract`, to keep automation windows visible in the saved Tesseract project and prevent duplicate project windows.
- Decision - The automation must use a singleton lock file before queue selection so duplicate or overlapping runs skip instead of processing the same triad.
- Decision - The lock stale threshold is 90 minutes, and healthy runs must refresh the lock heartbeat during major milestones.
- Decision - Temporary sprite-generation matte/background should be magenta `#FF00FF` when needed, never lime/green, and final output must be true transparent RGBA.
- Decision - Each creature requires a finishing pass for matte spill and cutout outline artifacts before final QA.
- Decision - The recurring sprite-sheet automation is paused after full queue completion.
- Warning - For robotics sheets, soft magenta removal before repack is safer than a direct hard repack because the direct path can preserve purple edge contamination.
- Warning - The automation must stop on QA failure or ambiguity instead of pushing through the queue.
- Warning - Do not launch this automation from Unity folders, the main game project, or the orchestration workspace; use the saved Tesseract Codex project.
- Source: User request, 2026-05-12.
- Source: [[short-term/2026-05-17-twb-creature-spritesheet-auto-ro-13]]
