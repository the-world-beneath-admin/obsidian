# TWB Trenchworks Lane Setup

## Status

Complete - 2026-05-15.

## What Changed

- Created project folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks`.
- Created starter subfolders:
  - `docs`
  - `research`
  - `prototype`
- Created orchestration worker folder: `C:\Users\yrred\Documents\New project 2\twb-trenchworks-worker`.
- Created worker hydration prompt: `C:\Users\yrred\Documents\New project 2\twb-trenchworks-worker\HYDRATION_PROMPT.md`.
- Added project-scoped worker agent: `C:\Users\yrred\Documents\New project 2\.codex\agents\twb-trenchworks-worker.toml`.
- Created the Obsidian lane under `memory/wiki/twb-trenchworks/`.
- Created active task brief: `memory/briefs/current-twb-trenchworks-task.md`.

## Scope Decision

TWB Trenchworks is scoped as a standalone Unity 2D game under the The World Beneath umbrella. It is not a browser game and not a Phaser/Vite World Key.

## Next Gate

Hydrate the TWB Trenchworks worker for research and planning only. The worker should stop after writing its report and return control to Bob/orchestrator before any implementation.
