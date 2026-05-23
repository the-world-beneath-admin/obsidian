# Memory Curation Report - 2026-05-13 - Shared Platform BobNet Removal Decommission Intake

## Source Reviewed

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-shared-platform-bobnet-removal-final-decommission-report.md`

## Promoted To Permanent Memory

- Promoted source-side Bob/BobNet package-hub removal status.
- Promoted the existence and purpose of `migrations\0016_remove_retired_package_hub.sql`.
- Promoted the production gate: remote migrations `0015` and `0016`, optional secret deletion, Worker deploy, and live verification still require explicit approval.
- Promoted the warning that `BOB_FORGE_ADMIN_PASSWORD` remains as a live Cloudflare secret and must not be deleted casually.
- Promoted reported checks: JS syntax checks, Wrangler dry-run, local D1 migration, remote migration list, and inconclusive Wrangler dev smoke.
- Updated shared-platform memory to note that `SHARED_GAME_PLATFORM_PLAN.md` and `TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md` now exist.

## Not Promoted

- Temporary `%TEMP%` log file names.
- Failed Wrangler dev mechanics beyond the actionable warning.
- Broad chat narration.
- Full dirty file inventory beyond source areas that matter for the next gate.

## Remaining Blockers

- Remote D1 migrations `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql` require approval.
- Live deploy requires approval.
- Optional deletion of `BOB_FORGE_ADMIN_PASSWORD` requires approval.
- Served preview should be retried if visual/browser confirmation is required.

## Next Recommended Gate

Run a narrow production-readiness worker task to review the diff, retry served preview if desired, and prepare an explicit user-approved live cleanup sequence.
