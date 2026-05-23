# File Structure and Export Rules

## Purpose

This document defines how the factory side should be organized.

---

## 1. Root structure

Use this structure unless the existing project already has a better convention:

```text
Assets/TWB/Factory/
  Art/
    Source/
      Materials/
      Machines/
      Belts/
      Pipes/
      Items/
      VFX/
      UI/
    Generated/
      Floors/
      Machines/
      Belts/
      Pipes/
      Items/
      VFX/
      UI/
    Materials/
    Sprites/
  Prefabs/
    Buildings/
    Belts/
    Pipes/
    Items/
    UI/
  Scripts/
    Core/
    Grid/
    Logistics/
    Machines/
    Recipes/
    Visuals/
    UI/
    Editor/
  Data/
    Buildings/
    Items/
    Recipes/
  Scenes/
  Docs/
```

---

## 2. Naming rules

Use lowercase snake_case for asset names where possible.

Examples:

- `factory_floor_compacted_dirt_v001.png`
- `factory_belt_straight_h_v001.png`
- `factory_pipe_corner_ne_v001.png`
- `factory_machine_extractor_v001.png`
- `factory_machine_processor_v001.png`
- `factory_item_ore_chunk_v001.png`
- `factory_ui_status_no_power_v001.png`

---

## 3. Prefix rules

### Factory floor
- `factory_floor_`

### Machines
- `factory_machine_`

### Belts
- `factory_belt_`

### Pipes
- `factory_pipe_`

### Items
- `factory_item_`

### VFX
- `factory_vfx_`

### UI
- `factory_ui_`

### Prefabs
- `prefab_factory_`

---

## 4. Source vs generated

Keep image-generation or hand-source files in:

```text
Art/Source/
```

Keep Codex-generated placeholder art in:

```text
Art/Generated/
```

Do not mix source and processed outputs.

---

## 5. Data asset naming

Examples:

- `item_ore_chunk.asset`
- `item_metal_parts.asset`
- `item_ammo_crate.asset`
- `recipe_ore_to_metal_parts.asset`
- `recipe_metal_parts_to_ammo_crate.asset`
- `building_extractor.asset`
- `building_processor.asset`
- `building_workshop.asset`

---

## 6. Sprite import expectations

Factory sprites should use consistent:

- pixels per unit
- pivot rules
- compression settings
- filter mode
- atlas grouping

Exact values can match the existing project, but Codex must keep them consistent.

---

## 7. Pivot rules

- floor tiles: center
- belts: center
- pipes: center
- machines: footprint center
- item tokens: center
- VFX: emission origin or center
- UI icons: center

---

## 8. Export standard

Each generated asset family should be documented with:

- purpose
- file path
- expected size
- sprite mode
- prefab usage
- scene usage

---

## 9. Documentation requirement

Codex should keep implementation notes in:

```text
Assets/TWB/Factory/Docs/
```

At minimum:

- `factory_implementation_notes.md`
- `factory_validation_report.md`
