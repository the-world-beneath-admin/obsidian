# TWB Shared Platform Worker Report - 2026-05-13 - Hook-In Blocker Plan Step 1

## Task

Plan the blocker burn-down for hooking the main game and World Keys into the cloud-based account/inventory platform, then implement Step 1.

Scope: shared platform/account systems. No Unity, Garden, or Alchemy source files were modified.

## Result

Created a blocker burn-down plan in the website platform plan and implemented Step 1: the Unity snapshot endpoint no longer exports local Unity inventory into shared account inventory.

`/api/game/sync-snapshot` now behaves as a Unity profile snapshot/audit hook. It records the game profile and snapshot trail, but it sends empty shared inventory deltas for Unity `SoftCurrency`, `MaterialItems`, `CardItems`, and local `Companions`.

This preserves account attachment and cloud-save testing while protecting the shared-vs-local inventory boundary.

## Blocker Burn-Down Plan

1. Guard Unity snapshot sync so main-game local inventory cannot leak into shared platform inventory by accident. Completed locally.
2. Add server-authoritative export endpoints for World Keys, beginning with Glassroot Garden transfer bundles.
3. Define exact export catalog IDs, stack policy, account-bound policy, and idempotent event IDs for Garden, Alchemy, and main-game exports.
4. Add shared pet projection contracts for each game surface, including stat mapping, role use, and companion-lock requirements.
5. Add account UI/API controls to list and revoke linked game clients.
6. Remove or fully isolate leftover BobNet/Bob package source routes and schema once no longer needed.
7. Add Worker smoke checks for registration, starter awards, account state, game linking, save slots, and rejected unsafe inventory writes.

## Files touched

- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-shared-platform-blocker-plan-step1-report.md`

## Checks run

- `git diff --check -- worker.js TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md SHARED_GAME_PLATFORM_PLAN.md`
- `npx wrangler deploy --dry-run`

Both passed. Wrangler reported version `4.81.1` with update available `4.90.1`.

## Cleanup performed

No temporary files were created.

## Risks

- Unity UI text still says cloud save updates the shared inventory mirror; after this guard, the mirror update should show zero applied inventory deltas until explicit export endpoints are implemented.
- Existing live deployment is unchanged until a future approved deploy.
- Old `UNITY_SNAPSHOT_DELTA` ledger rows, if any, remain historical data. The endpoint now writes `UNITY_PROFILE_SNAPSHOT` going forward.
- Generic `/api/platform/inventory/events` still exists and still needs server-authoritative wrappers before public browser World Keys use it for rewards.

## Memory-worthy notes

- The intended hook-in order is now: read-only account attachment, then server-authoritative Garden export, then Alchemy/main-game export contracts.
- Main-game materials/cards should not become shared inventory through full-save mirroring.
- Explicit exports should be named, allowlisted platform items, not arbitrary client-provided deltas.

## Do not promote to memory

- Do not treat this as deployed live yet.
- Do not treat generic inventory events as production-safe World Key reward authority.

## Blockers

- Step 2 remains: design and implement Glassroot Garden server-authoritative transfer-bundle export.
- Shared pet projection and token revocation remain open.
- BobNet/Bob package cleanup remains a separate source cleanup gate.

## Next recommended gate

Approve local deployment of Step 1 if desired, then implement Step 2: a Garden-specific Worker endpoint that accepts a transfer-bundle completion request and calculates the shared platform item delta server-side.
