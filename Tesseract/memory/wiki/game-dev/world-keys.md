# World Keys

## Summary

World Keys are subgame or interface experiences connected to The World Beneath platform. They may share account, Companion, inventory, currency, lock, and ledger surfaces, but each World Key needs its own clear scope and server authority.

## Memory Items

- Fact - The Garden is the public title for the farming/garden World Key; older Glassroot Garden notes are internal or historical prototype references.
- Fact - The player names their own garden when first opening The Garden.
- Fact - The Alchemy Lab is the public title for the second planned free World Key. Current implementation lane: [[wiki/world-keys/the-alchemy-lab/overview]].
- Fact - The player names their own lab when first opening The Alchemy Lab.
- Fact - Older archaeology docs describe a browser mini game sharing Companions, inventory, crafting inputs, Will, and Companion lock state with the main Unity game.
- Fact - Browser clients are untrusted; backend/server routes should own rewards, Companion locks, progression, and inventory grants.
- Fact - Faction war and player faction mechanics belong to the main game, not the archaeology mini-game.
- Fact - Glassroot bundle outputs are currently designed for World Key shared storage, separate from main-game inventory.
- Source: [[memory/raw/game-design/main-game/Browser_Archaeology_Game_Implementation_Plan]]
- Source: [[memory/raw/game-design/glassroot/NEW_WINDOW_HANDOFF]]
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]

## Known World Key References

- The Garden: first planned public free World Key; public-facing farming/garden experience. Current implementation lane: [[wiki/world-keys/the-garden/overview]].
- The Alchemy Lab: second planned public free World Key; public-facing alchemy experience. Current source project: `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.
- Glassroot Garden: internal or historical name for the active farming World Key prototype; do not use as the public title unless the user changes the naming decision.
- Archaeology: older/retired or previous pilot reference; use carefully because current platform notes say older archaeology assumptions may be stale.

## Rule

World Key memory can inform the main game, but it must not create main-game design decisions by itself.
