# Project Hierarchy

## Summary

The parent project is **The World Beneath**. World Key: Glassroot Garden is a subgame / World Key experience inside that larger project, not the main game itself.

## Memory Items

- Fact - The main game project is **The World Beneath**.
- Fact - The main Unity prototype source is `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.
- Fact - The farming project source is `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Fact - The website/account platform source is `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site`.
- Fact - TWB Trenchworks is a proposed standalone Unity 2D project under the TWB umbrella at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks`.
- Fact - Glassroot Garden is a browser-native farming World Key subgame.
- Fact - World Key shared storage is separate from main-game inventory unless the platform explicitly promotes or syncs data.
- Decision - Website login and account creation are the root account identity path for shared platform systems.
- Decision - Pets are shared account companions; materials remain game-local unless explicitly exported through shared platform inventory.
- Decision - Obsidian memory must treat the main game as the parent design authority and Glassroot as a child/module.
- Warning - Do not let Glassroot SEO, mechanics, or constraints overwrite main-game design decisions.
- Source: [[memory/raw/game-design/main-game/MASTER_BOOTSTRAP_STAGE_1_DOCS_v8]]
- Source: [[memory/raw/game-design/main-game/TWB_SYSTEM_ARCHITECTURE_MAP]]
- Source: [[memory/raw/game-design/glassroot/NEW_WINDOW_HANDOFF]]
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]

## Current Structure

```text
The World Beneath
  Main Unity game
    Phase 3 content expansion
    Dungeon/combat/reward/crafting/apply systems
    Will / materials / catalysts / creature-card loop
    World map and account/platform surfaces

  World Key subgames
    Glassroot Garden
    Archaeology pilot / retired or older reference
    Future World Keys

  Standalone TWB-tagged games
    TWB Trenchworks
      Unity 2D factory/logistics and automated trench-war concept

  Shared platform/account systems
    Website login and account creation
    Shared account pets / companion cards
    Explicit shared inventory exports
    Per-game material inventories and save state
```

## Rule

Game-dev and marketing briefs must state whether they are for:

- Main game
- Glassroot Garden
- Another World Key
- Standalone TWB-tagged game
- Shared platform/account systems
