# Generated Factory Art Spec

## Purpose

This document defines the code-generated prototype art Codex should create.

The project must not depend on perfect external art before the factory side works.

---

## Generated art principles

Generated art should be:

- simple
- readable
- top-down/2.5D
- consistently lit
- correctly sized
- organized
- usable in prefabs

---

## Recommended texture sizes

These are suggested, not mandatory:

- 1x1 floor tile: 128x128
- belt tile: 128x128
- pipe tile: 128x128
- small item token: 64x64
- machine 2x2: 256x256
- machine 3x2: 384x256
- depot 3x3: 384x384
- UI icon: 64x64 or 128x128
- VFX sheet frame: 64x64 or 128x128

---

## Generated floor assets

Create:

- compacted dirt yard
- worn concrete pad
- metal plate tile
- loading pad tile
- ore patch
- oil stain decal
- tire mark decal

---

## Generated logistics assets

Create:

- belt straight horizontal
- belt straight vertical
- belt corner variants
- pipe straight horizontal
- pipe straight vertical
- pipe corner variants
- input/output port icons

---

## Generated machine assets

Create:

- extractor
- processor
- workshop
- storage depot
- frontline supply depot
- generator
- power pole or marker

Each machine sprite should include:

- base body
- top plane
- functional detail
- port indication
- status lamp area
- contact shadow

---

## Generated item assets

Create:

- ore_chunk
- metal_parts
- ammo_crate
- sandbag_kit
- fuel_can
- repair_parts
- shell_crate

---

## Generated status icons

Create:

- working
- missing_input
- output_blocked
- no_power
- storage_full

---

## Generated VFX

Create simple sprites or sprite sheets for:

- smoke puff
- dust puff
- sparks
- output pulse
- placement highlight

---

## Completion criteria

This spec is complete when generated art assets exist and can be assigned to prefabs without manual drawing.
