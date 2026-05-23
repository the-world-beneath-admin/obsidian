# Memory Curation Report - 2026-05-12 - Sprite Sheet Automation Setup

## Task

Prepare a recurring Codex automation for future Tier 1 creature sprite-sheet production after the test set is approved.

## Result

Created a permanent automation plan and a paused Codex automation for sprite-sheet production.

The automation is intentionally paused until the test chunk is approved. It is configured for hourly standalone workspace runs because detached Codex workspace automations use hourly cadence. To reduce total runtime, the automation should process up to two family triads per run.

## Files Changed

- `memory/wiki/twb-creature-spritesheets/automation-plan.md`
- `memory/index.md`
- `memory/hot.md`
- `memory/log.md`
- `memory/reports/memory-curation/2026-05-12-sprite-sheet-automation-setup.md`

## Automation

- Name: `TWB Sprite Sheet Triad Runner`
- ID: `twb-sprite-sheet-triad-runner`
- Status: `ACTIVE` as of 2026-05-12 after user approved the first sprite-sheet result.
- Cadence: hourly
- Work unit: up to two family triads / six creatures per run

## Memory-Worthy Notes

- Decision - Recurring sprite-sheet production should process up to two triads per hourly run.
- Decision - The automation was activated after the user approved the first sprite-sheet result.
- Decision - Use hourly standalone Codex automation rather than 30-minute thread heartbeat for production work.
- Warning - The automation must stop on QA failure or ambiguity instead of continuing through the queue.

## Do Not Promote

- Exact 30-minute standalone cadence, because current detached workspace automation support is hourly.
- More than two triads per run, because art generation and QA should remain bounded.

## Next Recommended Gate

Monitor the first automated run report in `memory/short-term/` and pause the automation if QA failures or repeated ambiguity appear.
