# Shared Platform Pet Catalog And Inventory

## Summary

The website Worker/D1 backend is the authority for World Key pet catalog entries and account-owned companion inventory.

## Current State

- `platform_pet_catalog` stores server-owned World Key pet entries.
- `platform_companion_cards` stores account-owned pet inventory.
- Garden-compatible clients should read from `/api/platform/world-keys/garden/pet-catalog` and `/api/platform/pets` rather than local shop data.
- Garden purchases should use `POST /api/platform/world-keys/garden/pets/purchase`.
- `glassroot_garden_token` is the current Garden pet purchase currency.
- The seeded catalog currently contains 15 Glassroot Garden pets.
- Owned Garden companions expose normalized fields including `baseStats`, `gameProjection`, `state`, `role`, `focus`, `affinity`, `worldKeySkills`, `imageUrl`, and `iconUrl`.
- Default owned-pet Garden subskill state uses `worldKeySkills.glassrootGarden.subSkills.gardening`.

## Next Gate

- Define Garden token earning and export rules, then wire the Garden sync worker to the platform read/purchase APIs after remote migration and deploy approval.

## Sources

- `memory/short-term/2026-05-18-shared-platform-pet-catalog-inventory-report.md`
