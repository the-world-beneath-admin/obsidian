# Alchemy And Main Unity Local Hardening Pass - 2026-05-17

## Scope

Third Codex project-hardening implementation gate.

- The Alchemy Lab World Key browser project: `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`
- The World Beneath main Unity project: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`

## What Changed

The Alchemy Lab:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`.
- Added `docs/testing.md`.
- Added `docs/conventions.md`.
- Added `docs/common-pitfalls.md`.
- Added a real `npm run typecheck` script using `tsc`.

The World Beneath main Unity:

- Added root `AGENTS.md`.
- Added `Documentation/Codex/architecture.md`.
- Added `Documentation/Codex/testing.md`.
- Added `Documentation/Codex/conventions.md`.
- Added `Documentation/Codex/common-pitfalls.md`.
- Pointed future workers at the existing Unity automation wrapper instead of adding a second runner.

## Verification

The Alchemy Lab:

- `npm run typecheck` passed.
- `npm run build` passed.
- Vite reported the existing large chunk warning for the Phaser bundle.

The World Beneath main Unity:

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with `0` warnings and `0` errors.
- `dotnet build Backend\TWB.Backend.sln` passed with `0` warnings and `0` errors.
- `dotnet run --project Backend\TWB.Backend.Foundation.Tests\TWB.Backend.Foundation.Tests.csproj` passed with `11` backend foundation checks.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` reported `probably-clean`, `0` error signals, and `0` warning signals.

## Safety Notes

- The Alchemy Lab is not currently a git repository.
- The main Unity project already has a very large dirty git state from prior work. This pass only added `AGENTS.md` and `Documentation/Codex/`.
- No Unity gameplay/source files, assets, remote account systems, migrations, deployments, or browser World Key code were changed from the main Unity lane.
- Unity batch compile/edit-mode checks were documented but not run during this pass; the non-invasive status check was run.

## Memory Promoted

- Updated the Codex hardening standard with the third completed gate.
- Updated build/test command memory with the new Alchemy typecheck and main Unity local docs.
- Updated the active hardening task brief.
- Updated `hot.md`, `index.md`, and `log.md`.

## Remaining Blocked

- The Alchemy Lab still lacks dedicated unit/browser tests.
- The Garden still lacks dedicated lint/test scripts.
- Main Unity live Play Mode remains required for scene/UI/runtime behavior; solution and backend checks do not prove visual flows.
- The main Unity git worktree remains dirty outside this pass.

## Next Recommended Gate

Move from entry-doc hardening to verification-depth hardening:

- Add real automated tests or smoke harnesses only where they verify meaningful behavior.
- First candidates: Alchemy import/brew/cave/reload flow and Garden Notice Board/Bundler lifecycle.
- Do not add fake lint/test scripts just to satisfy command names.
