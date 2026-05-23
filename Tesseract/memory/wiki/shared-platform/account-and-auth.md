# Shared Platform Account And Auth

## Decisions

- Decision - Players log in through the website.
- Decision - Players create accounts through the website.
- Decision - The initial starter-pet selection happens during website account creation.
- Decision - The starter-pet selection is account-locked and should be offered only once.

## Existing Website Account Surface

Current known website files:

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\register\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\login\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\profile\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`

## Existing API Shape

Confirmed account/platform endpoints include:

- `/api/auth/register`
- `/api/auth/login`
- `/api/auth/logout`
- `/api/me`
- `/api/profile`
- `/api/inventory`
- `/api/platform/manifest`
- `/api/platform/state`
- `/api/platform/origin`
- `/api/platform/inventory/events`
- `/api/platform/game-saves/{gameId}/{saveKey}`
- `/api/game/link/start`
- `/api/game/link/approve`
- `/api/game/link/poll`
- `/api/game/link-device`
- `/api/game/sync-snapshot`

## Unity Attachment

Linked Unity sessions may read the platform mirror during UI/session initialization and Settings sync so account-selected starter pets and shared companions can appear in Archive/Card Summary.

The mirror is read-only in Unity until a separate import/export contract is approved. Local placeholder starter pets should not overwrite the mirror or imply authoritative account inventory.

Cloud-save loads over an existing active local profile now require a confirm step and a local backup before replacement. That guardrail stays Unity-side only; the website account flow still owns identity and starter selection.

## Implementation Rule

Do not create a separate login or account creation flow inside the main Unity game, The Garden, or The Alchemy Lab. They should attach to the website account/platform contract.

## Deployment Rule

Do not deploy account-system changes or apply remote D1 migrations without explicit user approval.

## Current Cleanup Gate

Bob/BobNet package-hub account/admin routes were removed from local source. Production cleanup still requires explicit approval for:

- remote D1 migrations `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql`
- live Worker deployment
- optional deletion of Cloudflare secret `BOB_FORGE_ADMIN_PASSWORD`

## Sources

- User clarification on 2026-05-12
- Website source inspection, 2026-05-12
- [[short-term/2026-05-13-twb-shared-platform-bobnet-removal-final-decommission-report]]
