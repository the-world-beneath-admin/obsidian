# Factory Vertical Slice Scene

## Purpose

Define the scene Codex should create to prove the factory side works.

---

## Scene path

Preferred:

```text
Assets/TWB/Factory/Scenes/FactoryVerticalSlice.unity
```

---

## Required scene layout

The scene should contain:

1. factory grid/floor
2. ore patch
3. extractor on or near ore patch
4. belt line from extractor to processor
5. processor
6. belt line from processor to workshop
7. workshop
8. belt line from workshop to frontline supply depot
9. frontline supply depot
10. generator/power source
11. UI canvas
12. camera configured for top-down view

---

## Test objective

The scene should demonstrate:

```text
ore_chunk -> metal_parts -> ammo_crate -> ammo_supply_counter
```

---

## Player/developer actions

Ideally the player can place buildings.
If not fully interactive yet, the scene may contain a prebuilt working chain plus build UI for future use.

A prebuilt working chain is acceptable for first proof.

---

## Scene readability checklist

At game zoom, a person should identify:

- resource patch
- extractor
- belt direction
- processor
- workshop
- depot
- moving items
- power source
- supply counter

---

## Acceptance criteria

The scene opens, runs, produces ammo supply, and visually explains the factory loop.
