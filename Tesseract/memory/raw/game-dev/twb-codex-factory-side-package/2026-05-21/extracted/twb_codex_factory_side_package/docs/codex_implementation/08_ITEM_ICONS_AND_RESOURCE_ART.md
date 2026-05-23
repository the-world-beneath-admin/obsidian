# Item Icons and Resource Art

## Purpose

Define item assets and resource nodes for Codex implementation.

---

## Required item definitions

Create data/assets for:

- ore_chunk
- metal_parts
- ammo_crate
- sandbag_kit
- fuel_can
- repair_parts
- shell_crate

Only the first three must be functional in the first chain.

---

## First chain item behavior

### ore_chunk
- produced by extractor
- consumed by processor

### metal_parts
- produced by processor
- consumed by workshop

### ammo_crate
- produced by workshop
- consumed by frontline supply depot
- increments ammo supply counter

---

## Resource node implementation

A resource node should provide:

- resource type
- remaining amount or infinite flag
- visual sprite
- occupied/usable lookup

First prototype can use infinite ore.

---

## Icons and tokens

Each item should have:

- UI icon
- belt token sprite

These can be the same sprite at first.

---

## Acceptance criteria

The player can visually distinguish ore chunks, metal parts, and ammo crates on belts and in UI.
