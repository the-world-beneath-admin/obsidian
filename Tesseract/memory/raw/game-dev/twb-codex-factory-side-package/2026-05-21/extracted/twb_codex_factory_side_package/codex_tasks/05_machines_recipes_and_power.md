# Task 05 — Machines, Recipes, and Power

## Goal

Make the factory actually produce wartime supplies.

---

## Required machine types

Implement these minimum building roles:

1. resource node
2. extractor
3. processor
4. workshop / assembler
5. storage depot
6. supply depot / frontline output depot
7. power source or simplified power network

---

## Required data model

Use data-driven definitions for:

- items
- recipes
- buildings
- machine roles

Prefer ScriptableObjects where appropriate.

---

## Minimum chain

Implement this:

```text
ore_node -> extractor -> ore_item
ore_item -> processor -> metal_parts
metal_parts + casing/supplies -> workshop -> ammo_crate
ammo_crate -> supply_depot -> frontline_supply_counter
```

The exact item names can change, but the chain must be visible and complete.

---

## Machine states

Every machine should be able to report:

- working
- missing input
- output blocked
- no power
- idle

---

## Acceptance criteria

This task is complete when:

- at least one full recipe chain works
- machines consume inputs and produce outputs
- machine state is visible or inspectable
- supply depot increments a supply counter or sends data to the battlefield side
