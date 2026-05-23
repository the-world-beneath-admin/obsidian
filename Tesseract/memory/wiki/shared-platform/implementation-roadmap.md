# Shared Platform Implementation Roadmap

## Gate 1 - Website Account Foundation

Goal: make the website account system own starter selection and shared account companion persistence.

Expected work:

- audit existing account/platform APIs and D1 schema
- add a starter-selection schema if needed
- define starter pet catalog data for account creation
- update `/register/` and `account.js` with a clear starter-pet selection UI
- ensure backend validation enforces exactly 1 ATK, 1 DEF, and 1 UTIL
- ensure selection can be made only once per account
- dry-run and local checks only; no deployment without approval

Status note: source-side account starter-pet work exists in the website tree, including `migrations\0014_account_creation_starter_pets.sql`, but production status depends on the live deployment/migration gate.

## Gate 2 - Shared Inventory Contract

Goal: document and test which inventory records are shared and which are game-local.

Expected work:

- define shared pet companion card contract
- define World Key transfer material contract
- define per-game save boundaries
- add API/client examples for The Garden and The Alchemy Lab

Status note: Garden transfer export source exists in `migrations\0015_garden_transfer_exports.sql`, but the remote migration is pending approval.

## Gate 2B - BobNet Retirement Production Cleanup

Goal: remove retired Bob/BobNet package-hub surfaces from production after source cleanup.

Expected work:

- review the BobNet retirement diff
- retry served preview if browser confirmation is required
- apply remote D1 migrations `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql` only after approval
- optionally delete `BOB_FORGE_ADMIN_PASSWORD` only after approval
- deploy the Worker only after approval
- live-verify account, register, profile, forum, inventory/platform, and admin routes
- confirm Bob package/catalog/console/admin routes are gone or return expected non-success responses

## Gate 2C - Admin Support And Ticketing

Goal: give the website an admin-only support desk and a game-facing report endpoint.

Status note: local foundation is implemented in the website repo. It adds admin member stats, manual email-prep/export, support-ticket D1 schema, public ticket submission, and admin ticket queue/update tools. No remote D1 migration or live deploy has been run.

Remaining work:

- manual admin-session browser smoke with seeded users/tickets
- add game-side Report Bug button/client helpers
- add rate limiting/abuse controls before broad public exposure
- plan provider-safe email sending only after consent, unsubscribe, rate limit, audit log, and provider decisions

## Gate 2D - Creator Commercial Licensing

Goal: define the creator-platform commercial license before Kickstarter messaging expands creator-platform expectations.

Status note: internal draft exists at [[creator-commercial-license-structure]]. It proposes Tier 0 community/noncommercial use, Tier 1 `$20/month` Creator Access, and Tier 2 Commercial Creator License after `$100,000` in TWB-attributable covered gross revenue over a trailing 12-month period, with a starting candidate royalty of `2%` above the threshold.

Remaining work:

- Bob approval of threshold and percentage
- legal/accounting review of covered gross revenue, royalty, audit, and tax language
- Kickstarter-safe reward wording
- public creator-policy wording
- billing/Stripe implementation plan only after terms are approved

## Gate 3 - Garden Attachment

Goal: let The Garden replace or wrap localStorage prototype storage with account-backed platform APIs.

Expected work:

- load authenticated platform state
- write game save via `/api/platform/game-saves/the-garden/default`
- emit herb bundle transfer events only when bundles are finalized
- use shared account companion cards instead of hardcoded local companions where practical

## Gate 4 - Alchemy Attachment

Goal: let The Alchemy Lab consume/export shared bundles and use account companions.

Expected work:

- import herb bundles from account-backed platform inventory
- export essence bundles through platform events
- persist local lab/cave state through game saves
- respect companion locks if pets are busy in another World Key

## Gate 5 - Main Unity Attachment

Goal: make the main Unity game consume the same account companion and inventory contract.

Expected work:

- verify game-device link flow
- verify `/api/game/sync-snapshot`
- map Unity companion cards and material snapshots into platform state
- keep main-game material inventory local unless explicitly exported

Status note: Unity source now has safety slices in place. Platform account state is presented as read-only account state instead of an adoptable shared-inventory mirror, and cloud-save load now requires a two-step confirmation with a local backup before replacing an active local profile. The next Unity attachment slice is read-only shared companion and starter-selection projection.

## Sources

- User requirement on 2026-05-12
- Website source inspection, 2026-05-12
- [[short-term/2026-05-13-twb-shared-platform-bobnet-removal-final-decommission-report]]
