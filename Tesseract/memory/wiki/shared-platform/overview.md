# Shared Platform Account And Inventory Lane

## Summary

This lane covers the account-backed shared platform for The World Beneath, the main Unity game, and browser World Keys.

## Authority

- Website account creation and login are the root identity path.
- The website Cloudflare Worker and D1 database are the current shared platform backend.
- World Keys and the main Unity game attach to the website account through platform APIs, not separate player identities.

## Current Source

- Website/account backend: `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`
- Main Unity project: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`
- The Garden World Key: `C:\Users\yrred\Desktop\Unity\TWB-Farming`
- The Alchemy Lab World Key: `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`

## Current State

The website already has:

- `/register/`, `/login/`, `/profile/`
- `/api/auth/register`, `/api/auth/login`, `/api/me`
- `/api/platform/manifest`, `/api/platform/state`, `/api/platform/origin`
- `/api/platform/inventory/events`
- `/api/platform/game-saves/{gameId}/{saveKey}`
- `platform_pet_catalog` and `platform_companion_cards` now cover Garden pet catalog and owned pet inventory
- D1 tables for platform inventory stacks, companion cards, companion locks, wallet balances, game saves, and game-device link requests
- browser client helper `assets/js/twb-platform-client.js`
- shared platform docs `SHARED_GAME_PLATFORM_PLAN.md` and `TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- account starter-pet migration `migrations\0014_account_creation_starter_pets.sql`
- Garden transfer export migration `migrations\0015_garden_transfer_exports.sql`

The website Worker/D1 path also now carries the account-scoped global achievements framework. Achievement definitions are server-owned, per-account progress is stored separately, and event submission is idempotent by source event. See [[global-achievements]].

The website also now owns the World Key pet catalog and account-owned pet inventory surface. Glassroot Garden should sync to platform read/purchase APIs rather than keep local shop authority. See [[pet-catalog-inventory]].

The website also now has a local admin-support foundation: admin member stats, manual email-prep/export, D1 support tickets, public ticket submission, and an admin ticket queue. It is not deployed yet, and real email sending remains blocked pending provider/consent/unsubscribe planning. See [[admin-support-ticketing]].

The website support-ticket surface is now in place locally: public ticket submission, admin queue review/update, admin member stats, and a manual email-prep export list. Email remains manual-prep only, not automatic sending.

Creator platform tier direction is now recorded: Tier 1 is a `$20/month` subscription, and Tier 2 is a commercial creator license for high-earning TWB-derived commercial use. The current draft recommends defining the threshold as `$100,000` in TWB-attributable covered gross revenue over a trailing 12-month period and using a small royalty/revenue share, currently `2%` above the threshold as the starting candidate. This is not final public legal/policy copy. See [[creator-platform-tiers]] and [[creator-commercial-license-structure]].

Unity-side attachment now uses a conservative read-only account-state projection: linked sessions can cache shared companions, exported stacks, and account-selected starter pets into runtime UI, while cloud-save loads over an existing active local profile require confirmation plus a local backup before replacement.

## New Requirement

During website account creation, each player must make a one-time account-locked starter pet choice:

- choose exactly 3 starter pets
- exactly 1 ATK, 1 DEF, and 1 UTIL
- show pet pictures and brief descriptions
- show clear `0/1 ATK`, `0/1 DEF`, and `0/1 UTIL` selection meters
- state clearly that this is a one-time account-locked choice and unchosen starter pets will no longer be available to that account after confirmation

## Current Next Gate

For Unity attachment, proceed with read-only platform account-state display and shared companion projection. Unity may pull account home, shared companions, exported stacks, locks, and cloud save listings, but must not adopt platform inventory into local Will/material/card inventory without an explicit import/export design.

For website/shared-platform production, run a production-readiness gate:

- review the BobNet retirement diff
- retry served preview if desired
- prepare remote D1 migration approval for `0015_garden_transfer_exports.sql` and `0016_remove_retired_package_hub.sql`
- keep `BOB_FORGE_ADMIN_PASSWORD` until deletion is explicitly approved
- do not deploy until explicitly approved

Next design gate: define the backend event contract, idempotency, conflict model, and lock lifetime policy for the eventual companion mutation path before any write is added.

Global achievements follow the same server-owned pattern. The next gate is to define the first concrete achievements and their validation rules before any player-visible achievements are exposed.

Unity cloud-save guardrails are now present in source: loading a cloud save over a local active profile requires confirmation and creates a local backup first. No production backend changes were made for this Unity slice.

Unity attachment now treats shared platform inventory as a read-only runtime projection. Linked sessions can surface shared companions and account-selected starter pets in Archive/Card Summary when the mirror exists, but remote writes remain blocked pending an explicit mutation protocol.

The website pet catalog and Garden purchase surface are implemented locally in the website repo, but Garden still needs a sync pass to consume those APIs after the token-economy rules are settled.

## BobNet Retirement

Bob/BobNet package-hub source has been removed from the local website/shared-platform source. See [[bobnet-retirement]].

## Sources

- [[wiki/world-keys/shared-inventory]]
- [[wiki/world-keys/pets]]
- [[wiki/twb-unity/starter-pets/overview]]
- [[wiki/twb-unity/starter-pets/contracts]]
- Website source inspection, 2026-05-12
- [[short-term/2026-05-13-twb-shared-platform-bobnet-removal-final-decommission-report]]
