# Build And Test Commands

## Summary

These are the confirmed or currently documented local commands for active TWB code lanes.

## Project Locations

- Fact - Main game / The World Beneath Unity project: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.
- Fact - Glassroot Garden World Key browser project: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Fact - The Alchemy Lab World Key browser project: `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.
- Fact - TWB Trenchworks Unity project: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Fact - TWB-Marketing desktop app project: `C:\Users\yrred\Desktop\Marketing\TWB-Marketing`.
- Fact - Website / shared account platform project: `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`.
- Fact - Codex orchestration workspace: `C:\Users\yrred\Documents\New project 2`.

## Main Game / The World Beneath

Run from:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype
```

- Build Unity solution without restore: `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
- Build backend: `dotnet build Backend\TWB.Backend.sln`
- Run backend foundation checks: `dotnet run --project Backend\TWB.Backend.Foundation.Tests\TWB.Backend.Foundation.Tests.csproj`
- Run backend dev service: `dotnet run --project Backend\TWB.Backend.Foundation\TWB.Backend.Foundation.csproj`
- Unity compile/import check: `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
- Unity edit mode tests: `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode`
- Narrow Unity edit mode tests: `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter SystemConsole`
- Unity status: `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status`
- Watch Unity editor log: `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode watch-editor-log`

## Glassroot Garden World Key

Run from:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Farming
```

- Install dependencies: `npm install`
- Run dev server: `npm run dev`
- TypeScript check: `npm run typecheck`
- Build: `npm run build`
- Preview built app: `npm run preview`
- Test command: none defined yet.
- Lint/format command: none defined yet.

Use `npm run build` as the current TypeScript/build check until dedicated tests are added.

## The Alchemy Lab World Key

Run from:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Alchemy
```

- Install dependencies: `npm install`
- Run dev server: `npm run dev`
- TypeScript check: `npm run typecheck`
- Build: `npm run build`
- Preview built app: `npm run preview`
- Local smoke URL currently reported as `http://127.0.0.1:5174/`.
- Test command: none defined yet.
- Lint/format command: none defined yet.

Use `npm run typecheck` and `npm run build` as the current automated checks until dedicated tests are added.

## Verification - Codex Hardening - Alchemy And Main Unity - 2026-05-17

- Fact - The Alchemy Lab now has local `AGENTS.md` and `docs/` entry docs.
- Fact - The Alchemy Lab `npm run typecheck` passed.
- Fact - The Alchemy Lab `npm run build` passed with the existing large Phaser/Vite chunk warning.
- Fact - Main TWB Unity now has root `AGENTS.md` and `Documentation/Codex/` entry docs.
- Fact - Main TWB Unity `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with `0` warnings and `0` errors.
- Fact - Main TWB Unity `dotnet build Backend\TWB.Backend.sln` passed with `0` warnings and `0` errors.
- Fact - Main TWB Unity backend foundation tests passed with `11` checks.
- Fact - Unity automation `status` reported `probably-clean`, `0` error signals, and `0` warning signals.
- Warning - Unity compile/edit-mode batch checks and live Play Mode were not run during this hardening pass.
- Source: [[reports/memory-curation/2026-05-17-alchemy-main-unity-local-hardening-pass]]

## TWB Trenchworks

Run from:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

- Open the project in Unity `6000.3.8f1`.
- Solution build: `dotnet build TWB-TrenchWorks.sln --no-restore`
- Canonical scene: `Assets\Scenes\TrenchworksPrototype.unity`.
- If Unity opens a blank scene, use `TWB Trenchworks > Open Prototype Scene`.
- Play Mode smoke: press Play and confirm the top bar reads `TWB Trenchworks`, the factory/war map controls work, and the base-health war tracker is visible.
- Asset import helper: `TWB Trenchworks > Assets > Apply War Sprite Import Settings`.
- Icon validation helper: `TWB Trenchworks > Assets > Validate War Icon Pack`.

Warning: no stable command-line Unity automation wrapper is recorded for Trenchworks yet. The next hardening pass should add or document one.

## Verification - Codex Hardening - 2026-05-17

- Fact - The Garden now has local `AGENTS.md` and `docs/` entry docs.
- Fact - The Garden `npm run typecheck` passed.
- Fact - The Garden `npm run build` passed with the existing Vite large chunk warning.
- Fact - TWB Trenchworks now has local `AGENTS.md` and `docs/` entry docs.
- Fact - `dotnet build TWB-TrenchWorks.sln --no-restore` passed in Trenchworks with 0 warnings and 0 errors.
- Warning - Trenchworks Play Mode/runtime visuals are not verified by `dotnet build`; use Unity Play Mode or menu checks for visual/runtime changes.
- Source: [[reports/memory-curation/2026-05-17-garden-trenchworks-local-hardening-pass]]

## TWB-Marketing Desktop App

Run from:

```powershell
cd C:\Users\yrred\Desktop\Marketing\TWB-Marketing
```

- Install dependencies: `npm install`
- Run desktop dev app: `npm run dev`
- Run web renderer only: `npm run dev:web`
- TypeScript check: `npm run typecheck`
- Build: `npm run build`
- Lint: `npm run lint`
- Tests: `npm test`
- Preview renderer: `npm run preview`
- Package Windows app folder: `npm run package:win`

## Website / Shared Account Platform

Run from:

```powershell
cd C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

- Wrangler dry-run: `npx wrangler deploy --dry-run`
- Preferred local verifier: `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1`
- Fast syntax-only verifier: `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -SkipWranglerDryRun`
- Local D1 migration check: `npx wrangler d1 migrations apply twb-core --local`
- Remote migration: do not run without explicit user approval.
- Live deploy: do not run without explicit user approval.
- Syntax checks used by recent cleanup: `node --check worker.js`, `node --check assets\js\site.js`, `node --check assets\js\account.js`

## Verification - Codex Hardening - Marketing And Website - 2026-05-17

- Fact - TWB-Marketing now has local `AGENTS.md` and `docs/` entry docs.
- Fact - TWB-Marketing `npm run typecheck` passed.
- Fact - TWB-Marketing `npm run lint` passed.
- Fact - TWB-Marketing `npm test` passed with `2` test files and `13` tests.
- Fact - TWB-Marketing `npm run build` passed.
- Fact - The website/shared platform now has local `AGENTS.md`, `docs/` entry docs, and `scripts\verify-local.ps1`.
- Fact - Website `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1` passed with JavaScript syntax checks and Wrangler dry-run.
- Warning - Website remote D1 migrations and live deploy remain approval-gated.
- Source: [[reports/memory-curation/2026-05-17-marketing-website-local-hardening-pass]]

## Verification - 2026-05-11

- Fact - `npm run build` passed in `C:\Users\yrred\Desktop\Unity\TWB-Farming`, with a Vite large chunk warning.
- Fact - `dotnet build Backend\TWB.Backend.sln` passed in `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.
- Fact - `dotnet run --project Backend\TWB.Backend.Foundation.Tests\TWB.Backend.Foundation.Tests.csproj` passed with 11 backend foundation checks.
- Fact - Unity batch compile/edit-mode commands exist in `tools\unity-automation.ps1`, but they were not run during this setup pass.

## Verification - 2026-05-12

- Fact - `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` was reported passing after the Peggy/Stanly starter guardian validation fixes, with `0` errors and `4` existing warnings.
- Source: [[short-term/2026-05-12-twb-unity-worldmap-working-window-intake]]

## Verification - Main Unity Reward Flow - 2026-05-16

- Fact - `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed after the HoloGlyph icon wiring and dungeon run reward/dev-complete changes, with `0` errors and `3` warnings.
- Fact - HoloGlyph icon import audit found material, catalyst, modifier, skill attack, skill defense, skill utility, and currency PNGs had Unity `.meta` files and were imported as single sprites.
- Warning - Unity batchmode compile/status may be blocked or noisy when another Unity instance has `TWB_Phase1_IdlePrototype` open; confirm log context before treating that as a compile failure.
- Source: [[short-term/2026-05-15-twb-unity-icon-wiring-audit-report]]
- Source: [[short-term/2026-05-15-twb-unity-run-rewards-dev-complete-report]]
- Source: [[short-term/2026-05-16-twb-main-game-worker-final-decommission-report]]

## Verification - Starter Pets - 2026-05-12

- Fact - Starter-pet intake reported successful project builds for `TWB.Domain.csproj`, `TWB.Services.csproj`, `TWB.UnityBridge.EditorTools.csproj`, and `TWB.UnityBridge.Tests.csproj` using `--no-restore`.
- Fact - Final full solution build should still be verified in the next starter-pet worker window after the latest Peggy/Stanly corrections.
- Source: [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]

## Verification - The Alchemy Lab - 2026-05-12

- Fact - `npm.cmd run build` was reported run for `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.
- Fact - Browser smoke checks were reported at `http://127.0.0.1:5174/`.
- Source: [[short-term/2026-05-12-twb-alchemy-working-window-intake]]

## Sources

- `memory/raw/game-design/glassroot/package.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\package.json`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Backend\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\README-unity-automation.md`
