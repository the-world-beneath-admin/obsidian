# Items, Resources, and Containers

## Purpose

This document defines the goods that move through the factory.

Items must be readable as belt tokens and UI icons.

---

## 1. Item design rules

Items should be simplified visual tokens.

Each item needs:

- item id
- display name
- icon sprite
- belt token sprite
- category
- optional stack size
- optional frontline supply value

---

## 2. Recommended first item chain

Use a small chain:

```text
ore_chunk -> metal_parts -> ammo_crate -> frontline_ammo_supply
```

Optional expansion:

```text
cloth_bundle + dirt_fill -> sandbag_kit -> frontline_fortification_supply
fuel_chunk -> fuel_can -> vehicle_supply
scrap -> repair_parts -> repair_supply
shell_casing + explosive_charge -> shell_crate -> artillery_supply
```

---

## 3. Resource node types

### Raw ore
- visual: clustered dark/gray chunks
- use: metal parts, shells, equipment

### Fuel / coal / oil substitute
- visual: dark patch or canister source
- use: power, vehicles, processing

### Scrap
- visual: metal debris pile
- use: repair parts, ammo casing

### Fill / sand / earth
- visual: light dirt/sand pile
- use: sandbag kits, fortification material

---

## 4. Container visuals

Containers help the player understand outputs.

### Required containers
- generic crate
- ammo crate
- shell crate
- fuel can
- parts bin
- sandbag bundle
- supply pallet

---

## 5. Icon readability

Icons should be:

- bold silhouette
- limited detail
- no tiny labels
- consistent shading
- distinguishable by shape first, color second

---

## 6. Belt token readability

Belt tokens can be slightly exaggerated.

A crate token may be larger than real scale so the player can see it.

This is acceptable.

---

## 7. Storage rules

Storage/depot systems should display:

- item count if selected
- visible crate stack if full enough
- warning if full/blocking output

---

## 8. Minimum deliverables

Create item definitions and icons for:

- ore_chunk
- metal_parts
- ammo_crate
- sandbag_kit
- fuel_can
- repair_parts
- shell_crate

Only the first three must work in the first chain.
The rest can be ready for expansion.
