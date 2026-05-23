# Main Game Overview

## Summary

The World Beneath main game is the parent project. The current local main-game source appears to be the Unity prototype at `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.

## Memory Items

- Fact - Project name in bootstrap authority docs: **The World Beneath**.
- Fact - Authority baseline: MASTER CONTROL v4.
- Fact - SaveVersion v9 is active and must not change.
- Fact - Determinism is required; replay must be identical.
- Fact - UI is non-authoritative and snapshot/projection-only.
- Fact - Phase 1 and Phase 2 are structurally complete enough for Phase 3 content expansion.
- Fact - Phase 3 content expansion is the active priority in the bootstrap docs.
- Source: [[memory/raw/game-design/main-game/MASTER_BOOTSTRAP_STAGE_1_DOCS_v8]]
- Source: [[memory/raw/game-design/main-game/MASTER_BOOTSTRAP_STAGE_3_MANIFEST_v8]]

## Phase 3 Start Areas From Bootstrap

- Content Pool Expansion: expand active pet, monster, skill, modifier, and craftable output pools.
- Dungeon Content Expansion: expand biome, family, encounter, and run-content breadth.
- Progression & Economy Expansion: deepen Will, materials, catalysts, recipes, and craft output relationships.

## Active Unity Implementation Lane

- [[wiki/twb-unity/overview]]
- [[wiki/twb-unity/world-map-territory-overlay]]
- [[wiki/twb-unity/starter-pets-guardian-angels]]
- [[wiki/twb-unity/ui-hologlyph-style]]

## Warnings

- Warning - Do not change SaveVersion v9 without explicit authority.
- Warning - Do not treat World Key subgame loops as the main-game loop.
- Warning - Main-game faction, dungeon, crafting, economy, and content-expansion decisions must be recorded separately from Glassroot decisions.
