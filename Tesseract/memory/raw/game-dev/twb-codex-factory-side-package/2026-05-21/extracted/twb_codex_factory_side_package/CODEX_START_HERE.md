# TWB Factory Side Codex Package
## Start Here

This package explains how to build the factory automation / logistics side of the game using the same scalable art system as the trench battlefield package.

This is not a request to copy Factorio's art, UI, assets, names, icons, or exact gameplay structure. In this package, "Factorio side" means:

- grid-based factory building
- resource extraction
- belts / pipes / simple logistics
- machines that transform inputs into outputs
- storage and supply depots
- production chains that feed the trench war
- clear readable automation visuals

The target is a complete-looking prototype that is simple, readable, and expandable.

---

## Core decision

The factory side must use the same production approach as the battlefield side:

1. material sheets
2. masks
3. modular machine parts
4. overlay decals
5. simple generated sprites
6. reusable animation strips
7. UI/status overlays
8. code-driven placement and assembly

Do not rely on one-off finished illustrations for every machine.
Do not try to create a perfect high-detail factory game with bespoke art.
Build a clean, tactical miniature factory system that looks complete at gameplay zoom.

---

## What Codex should build

Codex should create:

- factory floor art system
- grid placement system
- belt art and belt logic
- pipe art and pipe logic
- simple extractor / processor / assembler / depot machines
- resource nodes
- item icons and moving item tokens
- machine status overlays
- recipe data model
- factory-to-frontline supply bridge
- factory vertical slice scene

---

## Recommended usage

Read this package in this order:

1. `MANIFEST.md`
2. `docs/factory_pipeline/README.md`
3. `docs/factory_pipeline/01_FACTORY_ART_DIRECTION_BIBLE.md`
4. `docs/factory_pipeline/02_FACTORY_PIPELINE_RULES.md`
5. `docs/codex_implementation/00_MASTER_CODEX_TASK.md`
6. Start tasks in `codex_tasks/`

To run this in Codex, use:

```text
Read CODEX_START_HERE.md and MANIFEST.md.
Follow the package exactly.
Start with codex_tasks/01_audit_and_foundation.md.
Do not copy Factorio's exact art or UI. Build the TWB factory/logistics side using the documented mask-driven tactical miniature art pipeline.
```

For a single large implementation attempt, use:

```text
Read ONE_SHOT_CODEX_PROMPT.md and implement it.
```

---

## Quality target

The factory side is successful when a player can clearly see:

- this is a resource node
- this is an extractor
- this is a belt carrying items
- this is a pipe carrying fluid
- this machine is working / blocked / missing input / missing power
- this output is ammo, shells, sandbags, fuel, repair parts, or supplies
- this depot sends resources to the trench war

The art can be basic.
It cannot look random, broken, or unfinished.

---

## Final visual goal

A readable top-down 2.5D wartime production yard: compact machines, muddy factory floors, belts, crates, pipes, smoke, working status lights, resource piles, and supply depots feeding the front.
