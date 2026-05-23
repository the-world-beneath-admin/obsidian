# Memory Curation Report - 2026-05-12 - Sprite Sheet Automation Artifact Fix

## Source

- User request to reduce sprite-sheet automation to one package per hour and fix chroma/cutout artifacts.

## Automation Updated

- Updated Codex automation `twb-sprite-sheet-triad-runner`.
- Schedule remains hourly: `FREQ=HOURLY;INTERVAL=1`.
- Run limit changed to exactly one family triad package per run.
- Prompt now forbids starting a second triad in the same run.
- Prompt now requires magenta `#FF00FF` for any temporary solid/chroma matte and forbids lime/green matte backgrounds.
- Prompt now requires a finishing pass before final repack/acceptance.
- Prompt now treats matte spill, cutout halos, and colored edge fringe as QA blockers.

## Memory Updated

- Updated [[wiki/twb-creature-spritesheets/automation-plan]].
- Updated [[wiki/twb-creature-spritesheets/asset-contract]].
- Updated [[wiki/twb-creature-spritesheets/decisions]].
- Updated [[wiki/twb-creature-spritesheets/overview]].
- Updated [[briefs/current-creature-spritesheet-task]] to target `AE-05` / `arcane-engineering` / `industrial`.
- Updated `C:\Users\yrred\Documents\New project 2\twb-creature-spritesheets-worker\HYDRATION_PROMPT.md`.
- Updated `C:\Users\yrred\Documents\New project 2\.codex\agents\twb-creature-spritesheet-worker.toml`.

## Not Changed

- Did not modify generated sprite assets.
- Did not modify Unity runtime code.
- Did not manually edit `CHUNK_QUEUE.md`.

## Remaining Risk

- The finishing pass is now required by prompt and contract, but the exact image-processing implementation may still vary by worker unless a dedicated helper script is added or hardened.

## Next Recommended Gate

Let the next hourly automation run process `AE-05` only, then review the short-term report and visual output before allowing the queue to continue.
