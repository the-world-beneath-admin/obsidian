# Current Alchemy Lab Task

## Status

Active - refreshed 2026-05-22 for new worker hydration.

## Scope

- Parent project: The World Beneath.
- World Key: The Alchemy Lab.
- Source/project name: TWB Alchemy.
- Code directory: `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.

## Worker Role

`alchemy-lab-worldkey-worker`

## Goal

Run the next bounded prototype pass for The Alchemy Lab: verify the current cave/pet movement loop, keep the work inside `TWB-Alchemy`, and make only narrow fixes needed for cave feel, pet return/sleep timing, or obvious smoke-test blockers.

Do not integrate accounts, website routing, production shared inventory, main Unity project files, or final art pipeline in this milestone.

## Read First

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\slynyrd-pixelblog-reference.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\external-game-dev-resource-index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\world-keys.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\shared-inventory.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\pets.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-alchemy-lab\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-alchemy-lab\systems.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-alchemy-lab\decisions.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-alchemy-lab\testing.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\world-keys\the-alchemy-lab\open-questions.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\AGENTS.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\architecture.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\testing.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\conventions.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\common-pitfalls.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\ALCHEMY_WIREFRAME_IMPLEMENTATION_PLAN.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\src\scenes\AlchemyLabScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\package.json`

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- destructive cleanup, broad delete, or old zip backup deletion unless explicitly authorized

## Done Criteria

- Changes stay inside `C:\Users\yrred\Desktop\Unity\TWB-Alchemy` unless explicitly authorized.
- `npm run typecheck` passes after TypeScript/code changes when available.
- `npm run build` passes after code changes.
- Browser smoke test at `http://127.0.0.1:5174/` has no console errors.
- Cave/pet behavior matches current direction: top-down maze, no player-placed torch loop, staggered pet release, and sleep after shed return/unload.
- Any remaining localStorage/test-state caveats are reported.
- A report is written to `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`.

## Report Destination

`C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-alchemy-lab-worldkey-worker-report.md`
