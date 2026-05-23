# Shared Platform Global Achievements

## Summary

The website Worker/D1 backend now has a server-owned framework for account-scoped global achievements across TWB games.

## Current State

- `platform_achievement_catalog` stores server-owned achievement definitions.
- `platform_user_achievement_state` stores per-account progress and completion state.
- `platform_achievement_events` stores idempotent progress events using `(user_id, source_game_id, source_event_id)`.
- Games may submit future progress events, but the Worker only mutates achievement state when an active server-side definition exists and the event source or scope is allowed.
- Reward-grant fields are rejected in achievement events. Currency, inventory, companions, locks, and rewards must continue through server-validated reward/export endpoints.
- No gameplay achievement definitions were created yet.
- The remote migration `0017_global_achievement_framework.sql` is still pending approval.

## Files Touched

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0017_global_achievement_framework.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\twb-platform-client.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\profile\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\platform\twbPlatformClient.ts`

## Follow-Up

- Add the first concrete achievements only after validation rules are written.
- Keep reward-grant logic out of the achievement event path.

## Source

- `memory/short-term/2026-05-18-twb-global-achievements-framework-child-report.md`
