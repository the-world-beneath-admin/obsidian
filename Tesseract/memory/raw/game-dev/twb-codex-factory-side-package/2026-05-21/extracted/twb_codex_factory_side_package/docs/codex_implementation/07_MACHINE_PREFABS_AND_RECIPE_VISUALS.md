# Machine Prefabs and Recipe Visuals

## Purpose

Implement machine prefabs and data-driven production.

---

## Required data types

### ItemDefinition
Fields should include:

- id
- display name
- icon sprite
- belt token sprite
- category
- frontline supply category if applicable
- supply value if applicable

### RecipeDefinition
Fields should include:

- id
- display name
- inputs
- outputs
- process time
- required machine role
- power required bool

### FactoryBuildingDefinition
Fields should include:

- id
- display name
- category
- footprint
- prefab
- machine role
- default recipe if any
- input/output ports
- power requirement

---

## MachineController behavior

A machine should:

1. receive items into input buffer
2. check recipe requirements
3. start processing when inputs and power are available
4. progress over time
5. produce output into output buffer
6. push output to belt or storage
7. update visual state

---

## Machine states

Use an enum or equivalent:

```text
Idle
Working
MissingInput
OutputBlocked
NoPower
StorageFull
```

---

## Required machine prefabs

- extractor
- processor
- workshop
- storage depot
- frontline supply depot
- generator

---

## Recipe visuals

Selected machine panel should show:

- input icons/counts
- output icons/counts
- progress bar
- machine state

---

## Acceptance criteria

At least one complete recipe chain works and can be understood through visual state/UI.
