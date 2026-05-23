# Main Game Systems

## Summary

The main-game architecture revolves around deterministic domain services, combat/dungeon runtime, reward claims, inventory, crafting, ApplyV2, snapshots, affinity, and content expansion systems.

## Memory Items

- Fact - Core runtime loop: player input, UI command dispatcher, domain service, combat engine or inventory mutation, snapshot builder, UI rendering.
- Fact - UI never mutates domain state directly.
- Fact - Dungeon pipeline includes dungeon selection, run processing, enemy assembly, combat resolution, victory/defeat, session drops, reward claim, inventory apply, and snapshot refresh.
- Fact - Combat uses a tick engine with deterministic cooldown, trigger, damage, affinity, and death-condition resolution.
- Fact - Monsters and pets share the unified creature schema.
- Fact - Craft Create is authoritative and Will is the crafting currency.
- Fact - ApplyV2 uses a stage-to-commit model with one skill slot and five modifier slots.
- Fact - Main gameplay flows pass through dungeon/combat/reward/inventory/crafting/apply/snapshot/UI spine.
- Source: [[memory/raw/game-design/main-game/TWB_SYSTEM_ARCHITECTURE_MAP]]

## Content Expansion Surfaces

- Pet-card/support registries.
- Monster/content registries.
- Family, biome, and affinity support registries.
- Recipe discovery/fallback/catalyst pool surfaces.
- Reward-family and catalyst-family mapping surfaces.
- UI builders touched by Phase 3 content work.
- Source: [[memory/raw/game-design/main-game/MASTER_BOOTSTRAP_STAGE_2_CODE_v8]]

