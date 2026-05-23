# Memory Curation Report - 2026-05-12 - Sprite Sheet Automation Singleton Fix

## Source

- User reported that the hourly sprite-sheet runner appeared to create copies of itself in multiple project windows and that duplicate runs were trying to process the same folder.

## Automation Updated

- Updated Codex automation `twb-sprite-sheet-triad-runner`.
- Renamed display name to `TWB Sprite Sheet Single Runner`.
- Kept schedule hourly: `FREQ=HOURLY;INTERVAL=1`.
- Reduced configured workspaces from three paths to one path:
  - `C:\Users\yrred\Documents\New project 2`
- Added singleton lock requirement before queue selection:
  - `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\.sprite-sheet-runner.lock.json`
- Duplicate/overlapping runs must write a skipped-run report and stop if a fresh lock exists.

## Memory Updated

- Updated [[wiki/twb-creature-spritesheets/automation-plan]].
- Updated [[wiki/twb-creature-spritesheets/decisions]].
- Updated [[wiki/twb-creature-spritesheets/overview]].
- Updated [[briefs/current-creature-spritesheet-task]].
- Updated [[hot]] and [[index]].

## Diagnosis

The automation had multiple configured `cwds`: orchestration workspace, Unity project, and Obsidian vault. That can fan one cron automation out into multiple project/chat contexts. The same queue file then made each run target the same next pending folder.

## Not Changed

- Did not modify generated sprite assets.
- Did not modify `CHUNK_QUEUE.md`.
- Did not pause the automation; it remains active with the single-workspace and singleton-lock protections.

## Remaining Risk

- Runs already launched before this fix may still continue under their old prompt. They should be stopped manually if they are duplicated.

## Next Recommended Gate

Allow only the single updated hourly automation to continue. If duplicated old windows are still running, stop them before they mark or overwrite queue work.
