# TWB Shared Platform Worker Report - 2026-05-13 - Account Inventory Foundation

## Task

Implement Milestone 1 for the shared platform/account lane in `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site`: website-owned account creation, account starter-pet selection, shared account companion cards, and clear shared-vs-game-local inventory boundaries. Keep Unity, Garden, and Alchemy read-only. After local validation, deploy live only after explicit approval.

## Result

Implemented and deployed the website account creation foundation with one-time starter-pet selection.

Account creation now requires a starting home area and exactly three starter pets: one ATK, one DEF, and one UTIL. The Worker validates the selection server-side, records an immutable starter-selection row, awards the chosen pets as account-level companion cards, records a platform ledger event, and writes audit rows during registration.

The starter catalog uses the approved six-pet Unity roster:

- ATK: Stanly, Merlin
- DEF: Nova, Chuck
- UTIL: Peggy, Hazel

Each starter has image paths, base stats, attack/skill data, skill-card IDs, three modifier slots, short descriptions, and story blurbs. Registration UI renders pet cards with pictures, blurbs, stats, modifiers, role meters, and the one-time account-lock warning.

No Unity, Garden, or Alchemy source was modified. Live deployment was performed only after explicit approval.

Live deploy details:

- Remote migration applied: `0014_account_creation_starter_pets.sql`
- Worker deployed: `the-world-beneath-site`
- Worker version: `f271d007-8694-4f03-8c6f-0abb07027d3b`
- Custom domains: `the-world-beneath.com`, `www.the-world-beneath.com`

Post-deploy correction:

- Updated Peggy's starter card display image to use the in-game sprite path: `/assets/images/starter-pets/util-peggy-creature-special-ephemrial-spirit-peggy.png`.
- Updated local source migration seed plus local and remote D1 catalog rows.
- Updated related Peggy companion catalog payloads and any existing Peggy selection/card JSON by path replacement; remote checks showed no existing affected user rows were changed.
- Fixed the live profile page layout after account creation testing. The profile account panel now uses a wider one-column dashboard surface, and starter summary cards use larger, cleaner card layout to avoid broken pet names.
- Deployed profile layout fix as Worker version `98b92812-0a14-4b1c-b06a-12d0e9269cfd`.

## Files touched

- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\register\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\profile\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\js\twb-platform-client.js`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\assets\images\starter-pets\`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\migrations\0014_account_creation_starter_pets.sql`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-shared-platform-worker-report.md`

## Checks run

- `node --check worker.js`
- `node --check assets\js\account.js`
- `node --check assets\js\twb-platform-client.js`
- `git diff --check` passed with only normal Windows CRLF warnings.
- `npx wrangler d1 migrations apply twb-core --local`
- Local D1 count checks confirmed 6 starter pets, 2 per role, 6 companion catalog rows, 6 skill catalog rows, and 9 modifier catalog rows.
- `npx wrangler deploy --dry-run`
- `npx wrangler d1 migrations list twb-core --remote`
- `npx wrangler d1 migrations apply twb-core --remote`
- `npx wrangler deploy`
- Live `GET https://the-world-beneath.com/api/platform/starter-pets` returned 6 starter pets and two choices per role.
- Live `GET https://the-world-beneath.com/register/` returned HTTP 200 and contained the starter-pet registration copy/script.
- Live starter image check returned HTTP 200 with `image/png`.
- Live invalid duplicate-role starter signup was rejected with HTTP 400 and did not create a test user.
- Remote D1 check confirmed `codex-live-smoke-%@example.test` users count is 0.
- Live Peggy starter API check confirmed `imagePath` and `spritePath` both point to the in-game sprite.
- Live Peggy sprite asset check returned HTTP 200 with `image/png`.
- Live profile page check returned HTTP 200 and confirmed the cache-busted profile CSS plus `account-profile-panel` markup.
- Live profile CSS check returned HTTP 200 and confirmed the wider profile grid and starter summary rules are served.
- Local Wrangler dev smoke test at `http://127.0.0.1:8787`.
- `GET /api/platform/starter-pets` returned 6 pets and role requirements.
- Disposable local registration succeeded and returned 3 awarded companion cards, persisted starter selection, and Monmouth origin.
- Invalid duplicate-role starter selection was rejected with HTTP 400.
- Playwright browser snapshot confirmed registration UI loaded pet images, descriptions, story blurbs, modifiers, role meters, and enabled submit only after 1/1 ATK, 1/1 DEF, and 1/1 UTIL.

## Cleanup performed

- Removed the temporary local Wrangler dev log.
- Removed Playwright CLI snapshot artifacts from `.playwright-cli`.
- Stopped the local Wrangler preview process.
- Removed the disposable local test user from local D1 after the API signup check.

## Risks

- The migration adds non-optional registration behavior. This was mitigated by applying the remote migration before deploying the Worker.
- Existing accounts have no forced starter-pet backfill flow yet. They can still exist without `platform_starter_pet_selections`.
- Bob package/BobNet source code and historical migrations still exist outside this account milestone. The previous live data reset removed metadata rows, and README no longer presents Bob package metadata as active platform shape, but full source-level Bob Hub removal should be a separate cleanup gate.

## Memory-worthy notes

- Starter-pet account creation is now server-authoritative and atomic: users, profiles, origin, starter selection, companion cards, ledger, and audit entries are created in one registration batch.
- Starter pets are shared as account-level companion cards. Main-game and World Key material inventories remain game-local unless exported through `/api/platform/inventory/events`.
- Website profile now surfaces starter selection and richer companion-card rows.
- `assets/js/twb-platform-client.js` now includes `getStarterPets()`.

## Do not promote to memory

- Do not promote local test account details; they were removed.
- Do not promote Wrangler local dev port/log details.
- Do not promote local test-account details; none were retained.

## Blockers

No implementation or deployment blocker remains for account creation testing.

## Next recommended gate

Recreate `twbmain@gmail.com` with the admin bootstrap key, then create the personal player account through the normal registration flow and confirm the profile shows the three starter companion cards.
