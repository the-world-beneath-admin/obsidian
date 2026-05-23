# Current Shared Platform Task

## Status

Active - pet catalog and account-owned pet inventory framework complete; next gate is Garden sync contract and token rules.

## Scope

Shared platform/account systems across:

- The World Beneath website account system
- main Unity game
- The Garden World Key
- The Alchemy Lab World Key

## Project Authority

Website login and account creation are the root identity path.

Primary code target:

`C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`

Read-only integration targets:

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`

## Goal

Next milestone: define Garden token earning / export rules and wire the Garden sync worker to the website pet catalog and purchase APIs.

Keep Unity/Garden read-only for this pass until the sync contract is approved. The authoritative website/platform pet catalog and account-owned pet inventory framework is now implemented.

## User Requirements

- Players log in through the website.
- Players create accounts through the website.
- Starter-pet selection happens during account creation.
- Pets are shared across the account and all game inventories.
- World Keys and the main game have their own materials inventories unless a material is explicitly exported to shared platform inventory.
- The Garden should be able to attach to the account-backed system after skinning/polish.
- Starter selection must require exactly 1 ATK, 1 DEF, and 1 UTIL starter pet.
- The UI must show pet pictures, short descriptions, and clear `0/1` role meters.
- The UI must clearly state the choice is one-time and account-locked.
- Website/platform must expose pet catalog entries, account-owned pets, purchase cost, tier, affinity/focus, stats, lore, art references, and World Key availability.
- Website/platform pet catalog authority now lives in `platform_pet_catalog`; account-owned companions live in `platform_companion_cards`.
- Per-owned-pet World Key subskill state must use `worldKeySkills.glassrootGarden.subSkills.gardening = { level, xp, updatedAtUtc, statBonuses? }`.
- World Key subskills must remain separate from main-game pet balance/stats.
- Garden compatibility must preserve the existing companion card shape used by `companionCards`.
- No remote migrations, live deploy, or connected account/social/API automation in this pass.

## Read First

- [[hot]]
- [[index]]
- [[wiki/game-dev/project-hierarchy]]
- [[wiki/shared-platform/overview]]
- [[wiki/shared-platform/account-and-auth]]
- [[wiki/shared-platform/inventory-boundaries]]
- [[wiki/shared-platform/starter-pet-selection]]
- [[wiki/shared-platform/pet-catalog-inventory]]
- [[wiki/shared-platform/implementation-roadmap]]
- [[wiki/shared-platform/open-questions]]
- [[wiki/world-keys/shared-inventory]]
- [[wiki/world-keys/pets]]
- [[wiki/twb-unity/starter-pets/overview]]
- [[wiki/twb-unity/starter-pets/contracts]]

## Key Website Files

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\wrangler.jsonc`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\register\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\profile\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\twb-platform-client.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0010_shared_game_platform.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0011_platform_ledger_user_scoped_idempotency.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0012_game_device_link_flow.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0014_account_creation_starter_pets.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0015_garden_transfer_exports.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0016_remove_retired_package_hub.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\scenes\GlassrootGardenScene.ts`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\src\platform\twbPlatformClient.ts`

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\register\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\profile\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\twb-platform-client.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\SHARED_GAME_PLATFORM_PLAN.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\`
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\`
- remote D1 migrations
- live deployment
- Cloudflare secrets or production configuration changes
- destructive git operations, broad staging, blanket cleanup, reset, or revert

## Checks

From:

```powershell
cd C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

Recommended checks:

```powershell
npx wrangler deploy --dry-run
```

If a migration is added, run local migration checks only unless Bob/user explicitly approves remote changes:

```powershell
npx wrangler d1 migrations apply twb-core --local
```

Use served preview or Wrangler dev for UI checks when practical. Do not rely on direct `file://` preview.

Before any live cleanup, require explicit user approval for:

```powershell
npx wrangler d1 migrations apply twb-core --remote
npx wrangler deploy
```

Optional live secret deletion for `BOB_FORGE_ADMIN_PASSWORD` also requires explicit approval.

## Done Criteria

- Website API exposes pet catalog, owned pet inventory, and Glassroot Garden World Key pet purchase flow.
- Account UI shows owned pets, selected pet detail, and a Garden shop/catalog surface.
- Owned-pet World Key subskill state uses `worldKeySkills.glassrootGarden.subSkills.gardening = { level, xp, updatedAtUtc, statBonuses? }`.
- Main-game pet stats remain separate from World Key subskills.
- Garden sync contract changes and token earning rules are documented.
- Website build/test checks are run or exact blockers are reported.
- A report is written to `memory/short-term/`.
