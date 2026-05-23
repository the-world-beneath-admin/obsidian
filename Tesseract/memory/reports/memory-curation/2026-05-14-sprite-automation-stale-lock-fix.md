# Memory Curation Report - 2026-05-14 - Sprite Automation Stale Lock Fix

## Source Reviewed

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-creature-spritesheet-auto-skipped-lock-2026-05-14-084919.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-creature-spritesheet-auto-cy-07.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- `C:\Users\yrred\.codex\automations\twb-sprite-sheet-triad-runner\automation.toml`

## Problem

The sprite-sheet automation was blocked by a singleton lock for `CY-08` that had not produced a completion or blocker report. The next run skipped because the old automation rule waited 3 hours before considering a lock stale.

## Fix Applied

- Archived and removed the orphaned `CY-08` lock.
- Updated the Codex automation `twb-sprite-sheet-triad-runner` to keep running hourly but treat locks as stale/orphaned at 90 minutes instead of 3 hours.
- Added a lock heartbeat requirement to the automation prompt so healthy long runs refresh the lock after acquire, queue selection, each creature completion, and before final reporting.
- Updated the sprite automation memory page, overview, and current creature sprite task brief.

## Current State

- Automation remains `ACTIVE`.
- Launch workspace remains `C:\Users\yrred\Desktop\Obsidian\Tesseract`.
- Singleton lock is currently absent after cleanup.
- Latest completed reviewed chunk: `CY-07` / `cybernetics` / `park`.
- Next pending chunk: `CY-08` / `cybernetics` / `rural_agricultural`.

## Not Promoted

- Raw process list details.
- Low-level skipped-run formatting bugs such as literal `$lockPath` in the skipped report.

## Remaining Risks

- If a future healthy run exceeds 90 minutes without updating the heartbeat, the next run may treat it as stale. The heartbeat requirement is intended to prevent that.
- The automation should still be watched for the next run to confirm `CY-08` resumes correctly.

## Next Recommended Gate

Let the next scheduled `TWB Sprite Sheet Single Runner` process `CY-08`, or manually start the automation from the Tesseract project if an immediate run is desired.
