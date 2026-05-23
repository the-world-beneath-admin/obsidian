# Codex Project Hardening Standard

## Status

Active operating standard - created 2026-05-17.

## Purpose

Make each TWB code lane easier for Codex workers and child subagents to enter, verify, and report on without wasting context discovering project basics.

## Core Rule

Every active code project should make four things obvious:

- what the project is
- how it is structured
- how to run or verify it
- what not to touch

## Recommended Project Files

Each active repo or code folder should eventually have local entry-point docs. Use the repo's existing doc style where possible.

- `AGENTS.md` - project-specific scope, commands, allowed/forbidden areas, and do/don't rules
- `docs/architecture.md` - main systems, entry points, data flow, and ownership boundaries
- `docs/testing.md` - verification commands, manual smoke checks, known flaky checks, and log locations
- `docs/conventions.md` - naming, style, asset, UI, and state-management conventions
- `docs/common-pitfalls.md` - stale paths, dangerous commands, Unity locks, deployment traps, generated-art traps, and common false positives

Unity projects may use `Documentation/` instead of `docs/` when that is already the local convention.

## Verification Command Contract

Do not force every project into the same command names. Force every project into a clear verification contract.

JavaScript / TypeScript apps should prefer:

- `npm run dev`
- `npm run build`
- `npm run typecheck`
- `npm run lint`
- `npm test`
- `npm run preview`

Unity projects should prefer:

- a documented Unity version
- canonical scene path
- a `dotnet build` command when useful
- an edit-mode or Play Mode automation command when available
- a manual Play Mode smoke check when automation is not ready
- editor log path and common lock/blocker notes

Cloudflare/static website projects should prefer:

- local static preview command
- `node --check` commands for active JavaScript files
- `npx wrangler deploy --dry-run`
- local D1 migration checks where safe
- explicit warnings that remote migrations and deploys require user approval

## Do Not Fake Checks

Do not add placeholder scripts that pass while testing nothing. If a test/lint/typecheck command does not exist yet, either:

- document it as missing, or
- add a script that fails with a clear message until real coverage exists.

False confidence is worse than no test. A short pause; one permits oneself a sniff.

## Make Failure Easy To See

Each project should document:

- required local services
- common setup failures
- stale or renamed paths
- known flaky tests
- where logs are written
- how to tell a real failure from an expected local blocker
- whether build artifacts, screenshots, or logs should be cleaned up after the task

## Current Lane Assessment - 2026-05-17

- The Garden / Glassroot Garden has local `AGENTS.md`, `docs/` entry-point pages, and useful `npm run dev`, `npm run typecheck`, `npm run build`, and `npm run preview`; it still lacks dedicated lint and test scripts.
- The Alchemy Lab has local `AGENTS.md`, `docs/` entry-point pages, and useful `npm run dev`, `npm run typecheck`, `npm run build`, and `npm run preview`; it still lacks dedicated lint and test scripts.
- TWB-Marketing now has local `AGENTS.md`, `docs/` entry-point pages, `dev`, `dev:web`, `typecheck`, `build`, `lint`, `test`, `preview`, and `package:win`; local typecheck/lint/test/build passed on 2026-05-17.
- Main TWB Unity has root `AGENTS.md`, `Documentation/Codex/` entry-point pages, useful `dotnet` checks, backend tests, and `tools\unity-automation.ps1` entry points; live Play Mode is still required for scene/UI/runtime behavior.
- TWB Trenchworks has a helpful README, local `AGENTS.md`, local `docs/` entry-point pages, Unity menu helpers, and a passing `dotnet build TWB-TrenchWorks.sln --no-restore`; it still needs a command-line Unity automation wrapper if the lane is going to stay active.
- The website/shared platform now has local `AGENTS.md`, `docs/` entry-point pages, and `scripts\verify-local.ps1`; the verifier passed on 2026-05-17 with JavaScript syntax checks and Wrangler dry-run, while remote migrations and live deploys remain approval-gated.

## First Recommended Hardening Gate

The first Garden and TWB Trenchworks hardening pass was completed on 2026-05-17.

## Second Completed Hardening Gate

The TWB-Marketing and website/shared platform hardening pass was completed on 2026-05-17. Next hardening gate: The Alchemy Lab and the main TWB Unity project.

## Third Completed Hardening Gate

The Alchemy Lab and main TWB Unity hardening pass was completed on 2026-05-17. The major active code lanes now have local entry docs. Next hardening gate: verification depth, starting with real tests or browser smoke harnesses for World Key behavior rather than placeholder command scripts.
