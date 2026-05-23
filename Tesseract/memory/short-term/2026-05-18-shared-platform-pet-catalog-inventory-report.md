# Shared Platform Pet Catalog And Inventory Report

Date: 2026-05-18
Owner: Bob / orchestrator
Scope: shared website/platform account system, with Glassroot Garden read-only compatibility review

## Summary

Implemented the first website-authoritative shared pet catalog and account-owned pet inventory framework for The World Beneath.

The implementation uses Glassroot Garden's temporary local shop contract as the starting catalog shape, but keeps the authority in the website project:

`C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`

No Unity/Garden source files were edited.

## What Changed

- Added API routes for:
  - `GET /api/platform/pet-catalog`
  - `GET /api/platform/world-keys/garden/pet-catalog`
  - `GET /api/platform/pets`
  - `POST /api/platform/world-keys/garden/pets/purchase`
- Added platform pet catalog schema and seeded the 15 current Glassroot Garden shop pets.
- Added `glassroot_garden_token` as the Garden World Key pet purchase currency.
- Added purchase flow that checks account token balance, deducts tokens, creates `platform_companion_cards`, and writes a `WORLD_KEY_PET_PURCHASED` ledger row.
- Added API companion-card normalization so account pets expose:
  - `baseStats`
  - `gameProjection`
  - `state`
  - `role`
  - `focus`
  - `affinity`
  - `worldKeySkills` / `world_key_skills`
  - `imageUrl` / `iconUrl`
- Added default owned-pet World Key subskill state:

```json
{
  "worldKeySkills": {
    "glassrootGarden": {
      "worldKeyId": "glassrootGarden",
      "sourceGameId": "the-garden",
      "subSkills": {
        "gardening": {
          "level": 1,
          "xp": 0,
          "updatedAtUtc": "server timestamp"
        }
      }
    }
  }
}
```

- Added a profile-page account pet inventory UI with:
  - owned pet list
  - selected pet detail
  - Glassroot Garden pet shop/catalog
  - purchase buttons that respect current token balance
- Added platform client helper methods for pet catalog, owned pets, and Garden pet purchase.
- Updated the shared platform client contract with Garden sync requirements.
- Updated the active shared-platform task brief to match this milestone.

## Files Touched

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0018_platform_pet_catalog_inventory.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\migrations\0019_backfill_companion_world_key_skills.sql`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\profile\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\account.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\twb-platform-client.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\TWB_SHARED_PLATFORM_CLIENT_CONTRACT.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-shared-platform-task.md`

## Checks Run

From:

`C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`

- `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -RunLocalD1Migrations`
  - Passed.
  - Applied local migrations `0018_platform_pet_catalog_inventory.sql` and `0019_backfill_companion_world_key_skills.sql`.
  - Ran JavaScript syntax checks.
  - Ran `npx wrangler deploy --dry-run`.
- `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1`
  - Passed after the final route hardening patch.
- `npx wrangler d1 execute twb-core --local --command "SELECT COUNT(*) AS pet_count FROM platform_pet_catalog WHERE world_key_id = 'glassrootGarden';"`
  - Passed.
  - Returned `pet_count = 15`.
- `npx wrangler d1 execute twb-core --local --command "SELECT catalog_id, display_name, purchase_cost FROM platform_pet_catalog WHERE pet_id = 'shop-tend-dewbutton';"`
  - Passed.
  - Returned Dewbutton with cost `60`.
- Attempted an optional `wrangler dev --local --port 8799` route smoke check for `GET /api/platform/world-keys/garden/pet-catalog`.
  - Timed out while Wrangler was repeatedly reloading the local server.
  - The temporary Wrangler processes were identified and stopped.
  - This did not block the formal verification result above.

## Glassroot Garden Sync Contract

Garden should not use the local shop as production authority after the sync worker picks this up.

Next Garden sync worker should:

1. Fetch `GET /api/platform/world-keys/garden/pet-catalog`.
2. Fetch owned account pets from `GET /api/platform/state` or `GET /api/platform/pets`.
3. Map platform pets into the existing `companionCards` shape using `catalog_id`, `display_name`, `role`, `focus`, `baseStats`, `state`, `lore`/`summary`, and `worldKeySkills`.
4. Replace local shop purchase mutation with `POST /api/platform/world-keys/garden/pets/purchase`.
5. Treat `glassroot_garden_token` as the platform purchase currency once Garden token earning/export rules are defined.
6. Keep crop/material inventory local unless a server-allowlisted export endpoint exists.

## Risks And Notes

- Remote D1 migrations were not applied.
- No live deploy was performed.
- The account UI purchase button will be disabled until the account has `glassroot_garden_token`.
- Garden token earning rules are not defined yet.
- The seeded art references reuse current starter-pet art paths as placeholders. Final World Key pet art can replace those references without changing the companion-card contract.
- Main-game pet balance was not changed. World Key subskills remain separate from main-game stats.

## Memory-Worthy Notes

- `platform_pet_catalog` is now the website authority for World Key pet catalog entries.
- `platform_companion_cards` remains the account-owned pet surface.
- Owned account pets should always carry `worldKeySkills.glassrootGarden.subSkills.gardening`.
- Garden already has read-path compatibility for `worldKeySkills`, including the `glassrootGarden` key.

## Next Recommended Gate

Run a Garden sync worker that only integrates read/purchase API calls after remote website migration/deploy approval.

Before that worker starts, Bob should decide how Garden earns or receives `glassroot_garden_token`.
