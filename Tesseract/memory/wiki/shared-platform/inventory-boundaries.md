# Shared And Non-Shared Inventory Boundaries

## Summary

The platform needs separate inventory scopes so shared pets can move across experiences without flattening every game material into one global bucket.

## Shared Across Account

Shared account-level records:

- starter pets and other companion cards
- World Key pet catalog entries and account-owned pet inventory
- companion locks / activity commitments
- account identity, profile, and home origin
- platform wallet balances when explicitly shared
- platform inventory stacks when a game intentionally exports a reward or transfer item

## Game-Local Or World-Key-Local

Game-local records:

- main-game material inventory unless explicitly exported to the shared platform
- The Garden crop, raw plant, dried herb, plot, and local processing state
- The Alchemy Lab local lab storage, cave state, and unfinished crafting state
- World Key save blobs that are not meant to be spendable by other games

## Transfer Boundary

World Keys may export selected outputs to account-backed platform inventory through explicit platform events.

Examples:

- The Garden can export herb bundles to shared World Key storage.
- The Alchemy Lab can import herb bundles and export essence bundles.
- Local browser `localStorage` is prototype scaffolding only and must be replaced by account-backed APIs before production.

## Working Rule

Pets are shared account companions. Materials are not automatically shared. A material becomes shared only when the platform contract names it as a shared item and the game emits an idempotent platform inventory event.

The website pet catalog is authoritative; game-local shop contracts should be treated as compatibility layers only. Garden should pull catalog data from the platform and purchase through the platform endpoint instead of minting local authority.

Unity should treat pulled platform account state as read-only until an explicit import/export contract is approved. The current safe posture is to display account home, shared companions, exported stacks, locks, and cloud save listings without writing them into local Will/material/card inventory.

When a linked account mirror exists, Unity may project that state into its runtime cache so Archive and card surfaces show the account-selected starter pets instead of the old placeholder trio. If no mirror exists yet, the linked session should stay empty rather than invent local defaults.

Cloud-save loading now adds a local backup before replacement when an active profile exists. That protection is separate from inventory adoption and does not authorize shared inventory writes.

## Sources

- User clarification on 2026-05-12
- [[wiki/world-keys/shared-inventory]]
- [[wiki/world-keys/pets]]
- Website platform inventory source inspection, 2026-05-12
