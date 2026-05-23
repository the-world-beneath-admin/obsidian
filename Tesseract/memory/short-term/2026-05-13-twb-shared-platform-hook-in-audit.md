# TWB Shared Platform Hook-In Audit - 2026-05-13 - Cloud Account Inventory Readiness

## Task

Audit the live website-owned account and shared inventory platform before hooking in the main game and World Keys as a cloud-based account and inventory system.

Scope: shared platform/account systems. Main Unity, Glassroot Garden, and Alchemy were inspected read-only.

## Result

The platform is ready for account creation, starter-pet ownership, game-device linking, authenticated platform-state reads, and cloud save slots.

It is not ready for unrestricted production inventory hookup from the main game or browser World Keys. The current generic inventory event and Unity snapshot paths are useful scaffolding, but they are too broad to be public game authority without additional server-side export rules.

Recommended hook-in stance:

- Allow games to read account profile, origin, starter pets, companion cards, locks, and cloud saves.
- Do not let public browser World Keys mint rewards through generic `/api/platform/inventory/events`.
- Do not let the main Unity snapshot mirror all local materials/cards into shared platform inventory until an export allowlist exists.
- Treat shared pets as the first shared inventory class; keep game materials local unless a named export contract is approved.

## Files touched

Created this audit report only:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-shared-platform-hook-in-audit.md`

No website, Unity, Garden, or Alchemy source files were modified.

## Checks run

- Read current memory/hot/index/project hierarchy and shared-platform wiki pages.
- Inspected website Worker, schema migrations, client contract, and deployment config.
- Inspected main Unity account-link/cloud-save/cloud-mirror code read-only.
- Inspected Glassroot Garden and Alchemy storage/integration points read-only.
- Ran `npx wrangler deploy --dry-run` from the website project: passed.
- Ran `npx wrangler d1 migrations list twb-core --remote`: no migrations to apply.
- Queried live `/api/platform/manifest`: returned live schema, games, starter catalog, and starter-pet data.
- Queried live `/api/platform/starter-pets`: returned 2 ATK, 2 DEF, 2 UTIL starter pets with images, story blurbs, base stats, skills, and 3 modifier slots each.
- Checked live API CORS preflight: `204`, `Access-Control-Allow-Origin: *`, `Access-Control-Allow-Headers: content-type,authorization`.
- Attempted remote D1 count query with `wrangler d1 execute --remote`: blocked by Cloudflare API authorization error `7403`.

## Findings

### Ready

- Website account creation is now the authority for new accounts.
- Starter-pet selection is live, one-time, account-locked, and represented as account companion cards.
- Admin email config is `twbmain@gmail.com`; first-user admin auto-promotion is disabled.
- Game-device link flow exists and returns bearer tokens for non-browser/session clients.
- `/api/platform/state` exposes profile, origin, starter selection, wallet, inventory stacks, companion cards, locks, and saves.
- `/api/platform/game-saves/{gameId}/{saveKey}` can store per-game cloud save slots.
- API CORS allows bearer-token calls from browser-hosted World Keys.

### Blockers Before Full Hook-In

1. Generic inventory events are not game-rule authority.

`POST /api/platform/inventory/events` accepts caller-provided currency, item, companion, and lock deltas. It validates balance spending and companion lock ownership, but it does not prove that a Garden harvest, Alchemy cave run, or main-game reward actually happened. A public browser client must not be allowed to directly decide reward amounts.

Needed: game-specific server endpoints or an allowlisted event validator per game/export type. The browser should request actions or completed transfer proofs; the Worker should decide the platform deltas.

2. Unity snapshot sync currently mirrors too much into shared inventory.

`/api/game/sync-snapshot` reads Unity `SoftCurrency`, `MaterialItems`, `CardItems`, and `Companions`, diffs them, and writes platform ledger deltas. The Unity client also has UI text saying cloud save "mirrors inventory" and an importer that can adopt cloud inventory back into the local save.

This conflicts with the current boundary: main-game materials stay local unless explicitly exported to shared platform inventory.

Needed: disable or narrow material/card mirroring, or introduce a Unity export allowlist before letting the main game use this path as production sync.

3. World Key item export contracts are not final.

Glassroot Garden still uses `localStorage` save data and has transfer bundles conceptually moving to "World Key shared storage." Alchemy still uses `localStorage` for a prototype shared inventory key. Neither currently calls platform APIs.

Needed: define exact Garden and Alchemy export item IDs, quantities, event IDs, validation rules, and whether each exported item is account-bound, stackable, or local-only.

4. Shared pet gameplay semantics are not final.

The platform owns starter companion cards and lock rows, but Garden and Alchemy still use hardcoded local companion lists. Main/Garden/Alchemy need a shared pet projection contract: which account pets appear, how stats map, whether activity locks are mandatory, and whether pet levels/cooldowns are global or per-game.

5. Linked game-client token management is incomplete for production use.

Game-device linking exists, but there is no obvious user-facing list/revoke flow for linked game clients. Unity "Unlink" clears only local PlayerPrefs, not the server token.

Needed: account profile UI and API support to view/revoke linked clients before wider testing.

## Risks

- If browser World Keys call generic inventory events directly, players can craft arbitrary reward requests with their own bearer token.
- If Unity cloud mirror remains broad, main-game materials/cards can leak into shared inventory and then be adopted back into saves, muddling the shared-vs-local economy boundary.
- API CORS currently allows all origins for bearer-token calls. This is workable for cross-origin browser games, but production should pair it with strict token handling and server-side game validation.
- BobNet/Bob package source routes and tables still exist in Worker/migrations even though live package metadata was previously cleared. This is not the same as source cleanup.
- The Obsidian shared-platform wiki and brief are stale relative to the live deployment and need orchestrator review before being treated as current truth.
- Wrangler warned that version `4.81.1` has an update available to `4.90.1`.

## Cleanup performed

No temporary files were created.

## Memory-worthy notes

- Live starter pet catalog now has 6 starters: Stanly/Merlin ATK, Nova/Chuck DEF, Peggy/Hazel UTIL.
- Each live starter has a descriptive story blurb, skill/attack, base stats, and 3 starter modifier slots.
- Peggy's live `imagePath` and `spritePath` both use the in-game sprite file.
- Main Unity already has a website account link flow, bearer token storage, cloud state pull, cloud save slot save/load, and cloud inventory mirror/adopt code.
- Garden and Alchemy remain localStorage prototypes for materials/inventory and have no platform API calls yet.
- Cloud save slots look safe as per-game persistence; shared inventory mutation is the part needing stricter gates.

## Do not promote to memory

- Do not promote remote D1 row counts; the count query was blocked and no counts were confirmed in this pass.
- Do not promote the older brief's "no live deployment" restriction as current state; the system was already deployed live with user approval before this audit.
- Do not promote generic inventory events as production-safe authority for browser games.

## Blockers

- Add server-authoritative World Key export endpoints or validators.
- Narrow or disable Unity material/card mirror before production main-game sync.
- Define Garden/Alchemy/main-game export item contracts.
- Define shared pet projection and lock semantics per game surface.
- Add linked-client revoke/list UI and server endpoint.
- Decide whether CORS should remain wildcard for all API routes or be narrowed by platform route/use case.

## Next recommended gate

Build "Hook-In Gate 1: Read-Only Account Attachment."

Deliverables:

- Main game and World Keys can link/read account profile, origin, starter pet cards, and cloud saves.
- No game writes shared material inventory yet.
- Generic inventory event endpoint is treated as internal/scaffolding only.
- A new server-side export endpoint is designed for Glassroot Garden transfer bundles first, with fixed item IDs and Worker-side reward calculation.
- Unity `sync-snapshot` is narrowed to cloud save/profile/origin plus explicitly exported shared items only.
