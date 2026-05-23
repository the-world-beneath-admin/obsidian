# TWB System Architecture Map
Project: The World Beneath
Authority: MASTER CONTROL v4
SaveVersion: v9 (LOCKED)
Date: 2026-03-03

This document provides a **high-level architecture map of all major TWB systems** so they can be converted into diagrams, flow charts, or visual documentation.

The goal is to show **how each major system interacts with the others** without modifying the deterministic runtime architecture.

------------------------------------------------------------

# 1. Core Runtime Loop

PLAYER INPUT
    ↓
UI Command Dispatcher
    ↓
Domain Service (Dungeon / Crafting / Apply)
    ↓
Combat Engine or Inventory Mutation
    ↓
Snapshot Builder
    ↓
UI Rendering

The UI never mutates domain state directly.

------------------------------------------------------------

# 2. Dungeon Pipeline

Player selects dungeon parameters
    ↓
DungeonService.StartRun
    ↓
DungeonService.ProcessNextEncounter
    ↓
Enemy Assembly
    ↓
CombatMath.ResolveEncounter
    ↓
Victory / Defeat
    ↓
ResolveSessionOnlyDrops
    ↓
ClaimDungeonRewards
    ↓
InventoryService.ApplyAtomic
    ↓
Snapshot refresh

Key files
- Services/DungeonService.cs
- Domain/EnemyAssembly/*
- Domain/CombatMath/CombatMath.cs

------------------------------------------------------------

# 3. Combat System (Tick Engine)

Combat begins with two teams:

Player Team (CreatureSnapshot[])
Enemy Team (EnemySnapshot[])

Actors fire based on cooldown ticks.

Tick Loop

while encounter active:
    find actors whose cooldown expires
    resolve triggers in deterministic order
    compute damage
    apply affinity multipliers
    update HP
    check death conditions

Combat ends when:
- All enemies dead → victory
- Team HP ≤ 0 → defeat

Key files
- Domain/CombatMath/CombatMath.cs
- Domain/Combat/CreatureSnapshot.cs
- Domain/Combat/EnemySnapshot.cs

------------------------------------------------------------

# 4. Unified Creature System

Monsters and pets share the same schema.

CreatureBaseTemplate
    ↓
CreaturePrebuiltLoadoutTemplate
    ↓
ResolvedEnemyTemplatePayload
    ↓
EnemySnapshot

Identity hierarchy

TemplateId → species definition
LoadoutId → preset build
EnemyId → legacy mapping bridge

Key files
- Creatures/Unified/Templates/*
- Creatures/Unified/Resolution/*

------------------------------------------------------------

# 5. Crafting Create System

Recipe selected
    ↓
CraftingService.Execute
    ↓
Validate materials
    ↓
Consume materials
    ↓
Roll deterministic craft outcome
    ↓
Create outputs
    ↓
InventoryService.Apply

Durability rule
Tier 9/10 failures reduce durability by 10%.

Key files
- Services/CraftingService.cs
- Services/InventoryService.cs

------------------------------------------------------------

# 6. Crafting Apply System (ApplyV2)

ApplyV2 operates with a stage → commit model.

Stage phase
    UI selects creature
    UI selects skill/modifiers
    UiSimulationSession stores staged values

Commit phase
    UiCommandDispatcher
        ↓
    InventoryService
        ↓
    Attach skill/modifiers to card slots

Slots

1 skill slot
5 modifier slots

Key files
- Services/UIBoundary/UiSimulationSession.cs
- Services/UIBoundary/UiCommandDispatcher.cs

------------------------------------------------------------

# 7. Inventory System

Two inventory categories exist.

Material Inventory
    crafting materials
    dungeon resources

Card Inventory
    ItemInstance objects
    creature cards
    skill cards
    modifier cards

ItemInstance fields include

ItemInstanceId
ItemId
DurabilityBps
CreatureModifierSlots
CreatureSkillSlot

Key files
- Domain/Inventory/ItemInstance.cs
- Services/InventoryService.cs

------------------------------------------------------------

# 8. Snapshot Projection System

The UI receives read-only snapshots.

Domain State
    ↓
UiSnapshotService
    ↓
Snapshot DTOs
    ↓
UI Rendering

Snapshots include

DungeonUiSnapshot
CardSummaryUiSnapshot
CombatUiSnapshot

Key files
- Services/UIBoundary/UiSnapshotService.cs
- Domain/UIBoundary/*

------------------------------------------------------------

# 9. Affinity System

Affinity modifies final combat output.

Damage flow

Base damage
    ↓
variance/crit
    ↓
affinity multiplier
    ↓
final output

Multiplier sources

SkillAffinity vs MonsterAffinity
PetAffinity vs MonsterAffinity

Key files
- Domain/Combat/AffinityFinalOutputMultiplier.cs

------------------------------------------------------------

# 10. Biome System (Partial Infrastructure)

Enemies can include biome tags

example
biome:forest
biome:desert

DungeonPoolSelection already supports

BiomeTag

Missing piece

Biome registry defining allowed biomes.

Suggested base pool

forest
desert
jungle
plains
rural
urban
industrial

------------------------------------------------------------

# 11. Determinism Rules

All systems follow deterministic design rules

Stable ordering
No nondeterministic enumeration
RNG used only inside controlled sections
Replay identical results given same seed

Critical areas

CombatMath
Inventory mutations
Dungeon drop resolution

------------------------------------------------------------

# 12. High-Level System Interaction Map

Dungeon System
    ↓
Combat Engine
    ↓
Reward System
    ↓
Inventory System
    ↓
Crafting System
    ↓
ApplyV2 System
    ↓
Snapshot System
    ↓
UI

All gameplay flows pass through this spine.

------------------------------------------------------------

# End of Document

------------------------------------------------------------

# 13. Stat Rolling System (Certified)

Purpose:
- Provide deterministic base stat identities for **pets** (roll once + persist)
- Provide deterministic encounter variability for **enemies** (roll per dungeon slot; per-run only)

Core components:
- Domain/Stats/StatRollTables (hard-coded bands)
- Domain/Stats/BaseStatRoller (seeded deterministic roller)

Seeds:
- PET: Hash64("PET_STAT_ROLL", SaveSeed, PetInstanceId, Tier, Quality, AffinityId)
- ENEMY: Hash64("ENEMY_STAT_ROLL", DungeonRunSeed, WaveIndex, SlotIndex, EnemyId, Tier, Quality, AffinityId)

Persistence:
- Pets: persisted on instance (no reroll)
- Enemies: stored only on run actor / snapshot

Snapshot exposure:
- BaseHp/BaseMight/BaseMgk/BaseHaste are projection-only in UiSnapshotService outputs.

SystemConsole baseline:
- 146 / 146 GREEN

------------------------------------------------------------
