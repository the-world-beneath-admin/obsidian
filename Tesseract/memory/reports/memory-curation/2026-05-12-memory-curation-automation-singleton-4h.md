# Memory Curation Report - 2026-05-12 - Memory Curation Automation Singleton 4h

## Source

- User reported that the memory-curation automation was doubling itself into two windows on each run and requested changing the cadence to once every 4 hours.

## Automation Updated

- Updated Codex automation `twb-hourly-memory-curation`.
- Renamed display name to `TWB Memory Curation 4h Single Runner`.
- Changed schedule from hourly to every 4 hours:
  - `FREQ=HOURLY;INTERVAL=4`
- Reduced configured workspaces from two paths to one path:
  - `C:\Users\yrred\Documents\New project 2`
- Added singleton lock requirement before report review or memory promotion:
  - `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\.automation-locks\twb-memory-curation.lock.json`
- Duplicate/overlapping runs must write a skipped-run report and stop if a fresh lock exists.

## Memory Updated

- Updated [[wiki/memory/hourly-memory-curation-automation]].
- Updated [[hot]], [[index]], and [[log]].

## Diagnosis

The automation had multiple configured `cwds`: the orchestration workspace and the Obsidian vault. That can fan one cron automation out into duplicate project/chat contexts, causing two windows to review the same reports and risk duplicate memory edits.

## Not Changed

- Did not delete existing curation reports.
- Did not pause the automation; it remains active with single-workspace and singleton-lock protections.
- Did not rename the wiki file path, so existing links to [[wiki/memory/hourly-memory-curation-automation]] remain valid.

## Remaining Risk

- Runs already launched before this fix may continue under the old prompt. They should be stopped manually if duplicated.

## Next Recommended Gate

Allow only the updated four-hour single-run curation automation to continue. If old duplicate curation windows are still open, stop the duplicate before it edits memory.
