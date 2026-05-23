# Memory Curation Report - 2026-05-12 - Automation Launch Project Tesseract

## Source

- User clarified that the Tesseract folder has now been saved as a visible Codex project and requested automations happen there instead of in main project folders.

## Automations Updated

- Updated `twb-hourly-memory-curation`.
  - Display name remains `TWB Memory Curation 4h Single Runner`.
  - Schedule remains `FREQ=HOURLY;INTERVAL=4`.
  - Configured launch workspace changed to `C:\Users\yrred\Desktop\Obsidian\Tesseract`.
- Updated `twb-sprite-sheet-triad-runner`.
  - Display name remains `TWB Sprite Sheet Single Runner`.
  - Schedule remains `FREQ=HOURLY;INTERVAL=1`.
  - Configured launch workspace changed to `C:\Users\yrred\Desktop\Obsidian\Tesseract`.

## Memory Updated

- Updated [[wiki/memory/hourly-memory-curation-automation]].
- Updated [[wiki/twb-creature-spritesheets/automation-plan]].
- Updated [[hot]], [[index]], and [[log]].

## Rule

Active automations should launch from the saved Tesseract Codex project. They may still read/write other project files by absolute path when their scope allows it, but they should not use Unity folders, the main game project, or the orchestration workspace as their configured launch project.

## Remaining Risk

- Runs already launched before this change may still appear in older projects until stopped or completed.

## Next Recommended Gate

Watch the next scheduled automation launches and confirm they appear under the Tesseract project only.
