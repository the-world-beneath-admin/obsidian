# Current Codex Project Hardening Task

## Status

Entry-doc hardening complete for the major active lanes as of 2026-05-17. Verification-depth hardening remains open.

## Scope

Memory/workflow hardening across TWB code lanes.

## Goal

Make worker and child-subagent entry into active projects more reliable by adding local repo docs, visible verification commands, and common-pitfall notes.

## Read First

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\AGENTS.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\memory\multi-agent-orchestration-system.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\memory\codex-project-hardening-standard.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\build-test-commands.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`

## Completed First Gate - 2026-05-17

The Garden:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- Added real `npm run typecheck` alias.
- `npm run typecheck` passed.
- `npm run build` passed with the existing Vite large chunk warning.

TWB Trenchworks:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- `dotnet build TWB-TrenchWorks.sln --no-restore` passed with 0 warnings and 0 errors.
- Unity Play Mode remains a separate manual/Unity check for visual/runtime work.

## Completed Second Gate - 2026-05-17

TWB-Marketing:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- Added real `npm run typecheck` alias.
- `npm run typecheck` passed.
- `npm run lint` passed.
- `npm test` passed with `2` test files and `13` tests.
- `npm run build` passed.

Website / shared account platform:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- Added `scripts\verify-local.ps1`.
- `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1` passed, including `node --check` and Wrangler dry-run.
- Remote D1 migrations and live deploy remain blocked without explicit approval.

## Completed Third Gate - 2026-05-17

The Alchemy Lab:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- Added real `npm run typecheck` alias.
- `npm run typecheck` passed.
- `npm run build` passed with the existing large Phaser/Vite chunk warning.

Main TWB Unity:

- Added local `AGENTS.md`.
- Added `Documentation/Codex/architecture.md`, `Documentation/Codex/testing.md`, `Documentation/Codex/conventions.md`, and `Documentation/Codex/common-pitfalls.md`.
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with `0` warnings and `0` errors.
- `dotnet build Backend\TWB.Backend.sln` passed with `0` warnings and `0` errors.
- Backend foundation tests passed with `11` checks.
- Unity automation `status` reported `probably-clean`, with `0` error signals and `0` warning signals.

## Next Recommended Worker Gate

Verification-depth hardening for browser World Keys.

For The Alchemy Lab:

- Add a real browser smoke harness or focused tests for import, brew, cave expedition, reload persistence, and shared export flow.
- Do not add placeholder tests or lint scripts.

For The Garden:

- Add a real smoke harness or focused tests around Notice Board lifecycle, Transfer Bundles, Bundler/presentation, and save/reload behavior.
- Preserve existing manual build/typecheck gates.

For main TWB Unity:

- Consider a later Unity automation depth pass only after a narrow runtime target is chosen.
- Do not run broad Unity automation or live editor changes without a task-specific gate.

## Previous Recommended Worker Gate

Harden The Alchemy Lab and the main TWB Unity project.

For The Alchemy Lab:

- Add or update local `AGENTS.md`.
- Add `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- Consider adding a real `npm run typecheck` alias if `tsc` is already available through the local stack.
- Do not add fake passing test/lint scripts.

For main TWB Unity:

- Add or update a local `AGENTS.md` and concise entry docs if not already present.
- Document the canonical solution, backend checks, Unity automation wrapper, open-editor lock caveats, account/inventory boundaries, and live-editor verification expectations.
- Do not run destructive Unity cleanup, remote account mutations, or broad refactors.

## Earlier Recommended Worker Gate

Harden TWB-Marketing and the website/shared platform.

For TWB-Marketing:

- Add local `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- Consider adding a real `npm run typecheck` alias if it is not already present.
- Keep safety boundaries visible: no auto-posting, social APIs, private scraping, or account automation.

For website/shared platform:

- Add local `AGENTS.md` and/or `docs/` entry-point pages.
- Document safe local checks, `node --check`, Wrangler dry-run, local D1 migration checks, and explicit remote migration/deploy approval gates.
- Do not perform remote migrations or deploys.

## Original First Recommended Worker Gate

Harden The Garden and TWB Trenchworks first.

For The Garden:

- Add or update local project entry docs under `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Prefer `docs/architecture.md`, `docs/testing.md`, `docs/conventions.md`, and `docs/common-pitfalls.md`.
- Consider adding `npm run typecheck` as an alias for `tsc`.
- Do not add fake passing `npm test` or lint scripts.

For TWB Trenchworks:

- Add or update local docs under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Preserve the current README.
- Document Unity version, canonical scene, Play Mode smoke checks, menu helpers, and current lack of command-line automation.
- Do not create broad Unity automation until a narrow wrapper can be verified.

## Allowed Write Paths For A Future Worker

- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\src\`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\AGENTS.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\docs\`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\package.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\package.json`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- Any deployment, remote migration, git reset, or broad cleanup path.

## Done Criteria

1. Any added test or smoke command verifies real behavior.
2. The harness is documented in the relevant local `docs/testing.md`.
3. The command is run and the result is recorded.
4. A report is written to `memory/short-term/`.
