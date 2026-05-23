# Current Glassroot Garden New Player Experience Task

## Status

Active - created 2026-05-20 for a second Garden worker focused on tutorial, help, and first-login onboarding.

## Scope

- Parent project: The World Beneath.
- World Key: The Garden.
- Internal/source name: Glassroot Garden.
- Code directory: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Worker lane: `glassroot-garden-npe-worker`.

This is a Garden new-player-experience lane, not the bundling-machine art lane, not shared-platform backend work, not a main-game task, and not a deployment task.

## Goal

Design and begin implementing a new-player experience for The Garden:

- A first-login / first-open guided tutorial that introduces the core loop step by step.
- A reusable help/info reference system the player can open later.
- Player-facing tutorial/help scripts explaining planting, pet helpers, harvesting, storage, drying, bundling, Notice Board orders, Transfer Bundles, achievements, pet buying, account-linked pets, and future World Key material transfer.
- A narrow implementation plan and first safe code slice for tutorial/help UI inside the existing Phaser/Vite project.

## Current Gate

First gate: planning plus local implementation foundation.

The worker should:

1. Audit existing Garden UI/state hooks in `GlassrootGardenScene.ts` and related data/client files.
2. Draft a concise tutorial beat map and help-topic index.
3. Separate what is already live from what should be described as future-facing.
4. Recommend the smallest safe implementation foundation, such as a tutorial state machine, overlay shell, help menu shell, and persisted "tutorial completed" flag.
5. Implement only a narrow first slice after confirming it will not collide with the active bundling-machine/art worker.

## Read First

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\memory\multi-agent-orchestration-system.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\systems.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\testing.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-garden\open-questions.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\shared-inventory.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\pets.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\shared-platform\pet-catalog-inventory.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-19-glassroot-garden-worker-final-decommission-report.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\AGENTS.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\architecture.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\testing.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\common-pitfalls.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\platform\twbPlatformClient.ts`

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\*.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\output\playwright\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\assets\glassroot\garden\` unless the user explicitly approves asset work.
- Website/shared-platform source unless Bob/orchestrator explicitly creates a shared-platform task.
- Main Unity, Alchemy, Trenchworks, marketing app, sprite-sheet automation, or other project folders.

## Hard Rules

- Do not update permanent Obsidian memory.
- Do not create new art or image assets.
- Do not alter the failed v6 bundling-machine runtime path unless the user explicitly redirects this worker to that lane.
- Do not modify account/auth/backend/platform authority. Account-linked pets and future World Key transfer should be explained accurately from current contracts, not implemented here.
- Do not overpromise future systems as live. Mark future material transfer clearly as future-facing if it is not yet active.
- Preserve Notice Board one-off behavior and Transfer Bundle repeatability.
- Run `npm run build` after code changes.

## Recommended First Output

Before code, produce a short NPE plan for the user:

- Tutorial beat map.
- Help/info topic list.
- Proposed UI surfaces.
- What is live vs future-facing.
- First safe implementation slice.

## Done Criteria For Report

When the user asks this worker to report/decommission:

1. Summarize tutorial/help planning and implementation completed.
2. List changed files only.
3. Include the final tutorial beat map and help-topic index if changed.
4. Confirm live vs future-facing language choices.
5. Confirm `npm run build` result if code changed.
6. List screenshots/browser evidence if UI was implemented.
7. Explain cleanup performed.
8. Record risks and memory-worthy notes.
9. Recommend the next NPE gate.

## Report Destination

`C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-glassroot-garden-npe-worker-report.md`
