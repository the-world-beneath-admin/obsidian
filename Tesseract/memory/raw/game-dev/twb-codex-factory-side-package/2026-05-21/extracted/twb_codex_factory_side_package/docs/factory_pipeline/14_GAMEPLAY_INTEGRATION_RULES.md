# Gameplay Integration Rules

## Purpose

This document defines how the factory system should connect to gameplay.

The factory side is not just decoration. It must produce useful war supplies.

---

## 1. Core loop

The factory loop is:

```text
find resource
place extractor
move raw items
process raw items
assemble military supplies
store supplies
send supplies to front
use supplies in trench/battle systems
```

---

## 2. First prototype loop

Start with:

```text
ore_patch
  -> extractor
  -> ore_chunk on belt
  -> processor
  -> metal_parts on belt
  -> workshop
  -> ammo_crate on belt
  -> frontline_supply_depot
  -> ammo_supply_counter
```

This is enough to prove the system.

---

## 3. Data-driven recipes

Recipes should define:

- recipe id
- display name
- input items/counts
- output items/counts
- processing time
- required machine type
- optional power requirement
- optional fluid requirement

Do not hard-code recipes inside machine update loops.

---

## 4. Machine inventory rules

Machines should have small internal inventories:

- input buffer
- output buffer
- currently processing recipe
- timer/progress

If output is full, machine becomes blocked.

---

## 5. Belt item handling

Belts should not use physics for item movement.

Use deterministic movement:

- item has segment reference
- item has progress value
- item advances by speed * deltaTime
- segment transfers item to next segment when progress reaches end

---

## 6. Frontline supply counters

Factory outputs should become abstract war supplies.

Examples:

- ammo_crate -> ammo_supply +1
- sandbag_kit -> fortification_supply +1
- fuel_can -> fuel_supply +1
- repair_parts -> repair_supply +1
- shell_crate -> artillery_supply +1

These counters can be stored in a shared supply manager.

---

## 7. Factory-to-war integration

The battlefield side can consume supplies for:

- building trenches
- upgrading sandbag walls
- firing mortars/artillery
- deploying machine gun nests
- repairing vehicles or emplacements
- resupplying frontline units

This connection makes the factory side meaningful.

---

## 8. Avoid over-simulation early

Do not implement:

- full electrical grid complexity
- fluid pressure simulation
- exact inventory logistics for every crate
- worker AI logistics
- complex train systems
- hundreds of recipes

until the simple factory loop works.

---

## 9. Minimum completion rule

The factory side is gameplay-valid when:

- a resource becomes an item
- item moves through a belt
- machine transforms it
- another machine makes a war supply
- depot delivers that supply to a counter used by the rest of the game
