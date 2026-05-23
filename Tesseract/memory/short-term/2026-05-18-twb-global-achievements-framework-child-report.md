# TWB Global Achievement Framework Child Report

Date: 2026-05-18

Scope: Shared platform/account system, with a narrow Glassroot Garden World Key integration surface.

## Summary

Implemented the framework for account-scoped global achievements across TWB games.

Architecture:

- The website Worker remains the authority.
- `platform_achievement_catalog` stores server-owned achievement definitions.
- `platform_user_achievement_state` stores per-account progress/completion state.
- `platform_achievement_events` stores idempotent progress events using `(user_id, source_game_id, source_event_id)`.
- Games can submit future progress events, but the Worker only mutates achievement state when an active server-side definition exists and the event source/scope is allowed.
- Achievement events reject reward-grant fields. Currency, inventory, companions, locks, and rewards must continue through server-validated reward/export endpoints.

No gameplay achievement definitions were created.

## Files Changed

Website/shared platform:

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0017_global_achievement_framework.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\twb-platform-client.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\profile\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`

Garden:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\platform\twbPlatformClient.ts`

## Checks Run

Website/shared platform:

- `node --check worker.js` - passed
- `node --check assets\js\account.js` - passed
- `node --check assets\js\twb-platform-client.js` - passed
- `npx wrangler d1 migrations apply twb-core --local` - passed; applied `0017_global_achievement_framework.sql` locally
- `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -SkipWranglerDryRun` - passed
- `npx wrangler deploy --dry-run` - passed
- `npx wrangler d1 execute twb-core --local --command "SELECT COUNT(*) AS achievement_definitions FROM platform_achievement_catalog;"` - passed; returned `0`

Garden:

- `npm run typecheck` - passed
- `npm run build` - passed, with the existing Vite large chunk warning

## Cleanup

No temporary screenshots, scratch files, or throwaway logs were created.

## Risks

- Remote D1 migration `0017_global_achievement_framework.sql` has not been applied. Do not deploy Worker code that queries the new tables before the remote migration is approved and applied.
- The generic event endpoint intentionally records unmatched achievement events for audit/readiness, but it does not unlock anything unless an active server-owned definition exists.
- Future concrete achievements need game-specific validation before launch so clients cannot self-certify important milestones.
- The website repo already had a large dirty working tree before this pass; unrelated changes were not reverted.

## Memory-Worthy Notes

- Achievements should sit at the same platform authority level as shared pets/inventory: account-scoped, server-owned, and idempotent by user/source event.
- The first concrete achievement pass should define validation rules before adding player-visible achievements.

## Follow-Up Recommendations

- Apply `0017_global_achievement_framework.sql` remotely only after Bob/user approval.
- Add the first concrete achievements in a separate design/validation pass.
- Add smoke tests for duplicate achievement event submission once the Worker test harness exists.

## Boundary Notes

- Garden was edited only for dormant TypeScript interfaces and client methods.
- No Garden gameplay code calls the achievement endpoints.
- No Notice Board lifecycle or Transfer Bundle repeatability logic was altered.
- No achievement definitions were created.
- No permanent Obsidian memory was updated.
