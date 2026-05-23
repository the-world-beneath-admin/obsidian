# Codex Project Hardening Standard Report

Date: 2026-05-17

## Task

Review the user's proposed Codex robustness ideas and decide what should be implemented in the TWB orchestration system.

## Result

Promoted a project-hardening standard into permanent memory. The useful core is sound: Codex performs better when each project has clear entry docs, explicit commands, visible failure modes, and local conventions.

The recommendation is not to force every project into `npm test`. The correct standard is one reliable verification contract per project type.

## Findings

- The Garden and The Alchemy Lab have `npm run dev`, `npm run build`, and `npm run preview`, but no dedicated `typecheck`, `lint`, or `test` scripts.
- TWB-Marketing already has strong entry points: `dev`, `dev:web`, `build`, `lint`, `test`, `preview`, and `package:win`; it should add an explicit `typecheck` alias and local docs later.
- Main TWB Unity has useful `dotnet` commands and `tools\unity-automation.ps1`.
- Trenchworks has a good README and Unity menu helpers but lacks command-line automation docs.
- The website/shared platform has useful README notes, Wrangler dry-run, D1 local migration, and `node --check` checks, but no single local check script.
- The active marketing and website path is `C:\Users\yrred\Desktop\Marketing\...`, not the older misspelled `Markeing` path.

## Files Updated

- `memory/AGENTS.md`
- `memory/wiki/memory/codex-project-hardening-standard.md`
- `memory/wiki/game-dev/build-test-commands.md`
- `memory/briefs/current-codex-project-hardening-task.md`
- Active permanent memory and worker prompts that referenced `C:\Users\yrred\Desktop\Markeing\...`

## Memory-Worthy Notes

- Do not add fake passing test scripts. Missing tests should be documented honestly or fail with a useful message until real coverage exists.
- Make failure easy to see by documenting setup blockers, stale paths, known flaky checks, required local services, and log locations.
- The first recommended implementation gate is local docs/readiness hardening for The Garden and TWB Trenchworks.

## Next Recommended Gate

Spawn or hydrate a worker to add local `AGENTS.md` / `docs/` entry-point docs for The Garden and TWB Trenchworks, then report back to Bob for promotion.
