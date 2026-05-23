# Master Codex Task — Factory Side

## Mission

Implement the factory automation / logistics side of the game in Unity using the documented modular art system.

This factory side must produce supplies that can feed the trench battlefield side.

---

## What to create

### Systems
- factory grid
- placement controller
- generated art system
- conveyor belts
- item tokens
- machine recipes
- machine inventories
- storage/depot logic
- simple power/status logic
- factory UI
- frontline supply bridge

### Assets/prefabs
- floor tiles
- resource nodes
- belt prefabs
- pipe prefabs if practical
- extractor
- processor
- workshop
- depot
- generator
- item tokens/icons
- status icons
- simple VFX

### Scene
- `FactoryVerticalSlice` scene or equivalent

---

## Required gameplay chain

Implement this end-to-end:

```text
ore patch -> extractor -> ore chunk -> belt -> processor -> metal parts -> belt -> workshop -> ammo crate -> belt -> supply depot -> frontline ammo counter
```

This must work visibly.

---

## Required visual result

The scene should look like a complete prototype:

- factory floor exists
- machines have readable sprites
- belts show direction
- items visibly move
- machine statuses are readable
- UI explains selected buildings
- depot output is obvious

---

## Do not do

- do not copy Factorio's exact art/style/UI
- do not wait for final image assets
- do not use physics for belt logic
- do not make 100 recipes before one chain works
- do not make vague placeholder cubes with no readability
- do not delete existing trench/battlefield systems

---

## Recommended architecture

Use data-driven definitions:

```text
ItemDefinition
RecipeDefinition
BuildingDefinition
MachineController
BeltSegment
FactoryItemToken
FactoryGrid
FactoryPlacementController
FrontlineSupplyManager
```

Names may vary, but responsibilities must remain clear.

---

## Required final report

At completion, create or update:

```text
Assets/TWB/Factory/Docs/factory_validation_report.md
```

Include:

- files created
- files modified
- scene name
- how to test
- known issues
- next steps

---

## Success definition

The task succeeds when a player can open the factory vertical slice, watch items move through a small production chain, and see a frontline supply counter increase.
