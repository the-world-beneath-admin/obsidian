# Factory Pipeline README

## Purpose

This folder defines the factory/logistics half of the game.

The factory side must feel like the industrial engine behind the trench war:

- resources are extracted
- raw goods move by belts/pipes
- machines process goods
- workshops assemble military supplies
- depots send output to the front

This system should look complete while staying achievable with Codex-only production.

---

## Main rule

Build the factory from modular, reusable, top-down 2.5D parts.

Do not chase high-detail one-off machine art.
Do not copy Factorio's exact visual identity.
Make a custom wartime factory yard style that fits the trench game.

---

## Visual identity

The factory side should look like:

- small military-industrial yard
- muddy compacted floor
- belts, pipes, crates, bins
- squat utilitarian machines
- smoke, sparks, warning lights
- supply depots feeding the war
- readable icons and moving goods

---

## The factory art stack

Use the same layered logic as the battlefield package:

```text
base floor material
+ grid/placement readability
+ machine footprint masks
+ machine top sprites
+ pipe/belt layers
+ item tokens
+ decals
+ shadows
+ VFX
+ UI overlays
```

---

## Important documents

Read these first:

1. `01_FACTORY_ART_DIRECTION_BIBLE.md`
2. `02_FACTORY_PIPELINE_RULES.md`
3. `14_GAMEPLAY_INTEGRATION_RULES.md`
4. `15_TRENCH_FACTORY_BRIDGE.md`

Then read the Codex implementation docs.

---

## Prototype definition

A visually complete prototype needs:

- factory floor
- resource node
- extractor
- belt line
- processor
- workshop
- depot
- item icons/tokens
- basic power/status feedback
- simple VFX
- UI that explains what is happening

If that works, the factory side is production-ready enough for expansion.
