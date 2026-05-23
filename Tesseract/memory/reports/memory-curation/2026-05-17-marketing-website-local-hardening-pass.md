# TWB-Marketing And Website Local Hardening Pass - 2026-05-17

## Scope

Second Codex project-hardening implementation gate.

- TWB-Marketing desktop app: `C:\Users\yrred\Desktop\Marketing\TWB-Marketing`
- Website / shared account platform: `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`

## What Changed

TWB-Marketing:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`.
- Added `docs/testing.md`.
- Added `docs/conventions.md`.
- Added `docs/common-pitfalls.md`.
- Added a real `npm run typecheck` script using `tsc -b`.

Website / shared account platform:

- Added local `AGENTS.md`.
- Added `docs/architecture.md`.
- Added `docs/testing.md`.
- Added `docs/conventions.md`.
- Added `docs/common-pitfalls.md`.
- Added `scripts/verify-local.ps1` as the preferred local verification wrapper.

## Verification

TWB-Marketing:

- `npm run typecheck` passed.
- `npm run lint` passed.
- `npm test` passed with `2` test files and `13` tests.
- `npm run build` passed.

Website / shared account platform:

- `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1` passed.
- The verifier ran `node --check` against active JavaScript entry points.
- The verifier ran `npx wrangler deploy --dry-run`; no live deploy was performed.
- Wrangler dry-run reported `2642` asset files read and upload size `137.69 KiB / gzip: 27.58 KiB`.

## Safety Notes

- The website verifier keeps remote D1 migrations and live deploys behind explicit approval.
- TWB-Marketing docs preserve the manual/safety boundary: no auto-posting, no social account automation, no platform APIs, no private or gated scraping, no disguised advertising, and no fixed-interval posting.
- TWB-Marketing is not currently a git repository.
- The website repo already had unrelated dirty changes before this pass; this pass did not revert or stage them.

## Memory Promoted

- Updated the Codex hardening standard with the second completed gate.
- Updated build/test command memory with the new Marketing typecheck and website verifier.
- Updated the active hardening task brief.
- Updated `hot.md`, `index.md`, and `log.md`.
- Normalized the active log's canonical marketing path wording so future workers see `C:\Users\yrred\Desktop\Marketing\...`.

## Remaining Blocked

- Website live deploy, remote D1 migrations, and production changes remain blocked until the user explicitly approves them.
- TWB-Marketing can now verify locally, but future social/platform integration work still needs a platform-rules and account-permissions review first.
- The website repo's unrelated dirty state remains a separate source-control hygiene issue.

## Next Recommended Gate

Harden The Alchemy Lab and the main TWB Unity project next:

- Add local entry docs and explicit verification notes for `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.
- Add or tighten local entry docs for `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`, with emphasis on backend checks, Unity automation, open-editor lock caveats, and account/inventory boundaries.
