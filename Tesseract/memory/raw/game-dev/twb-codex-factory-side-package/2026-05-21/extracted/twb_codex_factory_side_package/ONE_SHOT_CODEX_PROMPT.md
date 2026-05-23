# One-Shot Codex Prompt

Use this prompt when you want Codex to make one full implementation pass.

---

## Prompt

You are implementing the factory automation / logistics side of this Unity game.
Read this package completely before modifying files:

- `CODEX_START_HERE.md`
- `MANIFEST.md`
- all files in `docs/factory_pipeline/`
- all files in `docs/codex_implementation/`
- all files in `codex_tasks/`

Build the factory side using the same mask-driven tactical miniature art system as the battlefield package.

Do not copy Factorio's exact art, UI, names, iconography, or assets. Use it only as a shorthand reference for "grid-based automation with belts, machines, resources, and logistics." This project needs its own wartime production-yard identity.

---

## Main deliverable

Create a complete playable factory vertical slice that includes:

1. factory floor / yard terrain
2. grid-based placement
3. resource nodes
4. extractor building
5. conveyor belts
6. pipe segments if practical
7. processor / smelter-style machine
8. assembler / workshop-style machine
9. storage depot
10. output depot that sends supplies to the trench/frontline side
11. simple item icons/tokens moving on belts
12. machine statuses: working, missing input, blocked, no power
13. power overlay or simple power network
14. basic UI for selecting and placing buildings
15. simple VFX: smoke, sparks, belt motion, machine activity
16. demo scene proving the full chain works

---

## Minimum production chain

Implement at least this chain:

```text
ore_node -> extractor -> belt -> processor -> belt -> workshop -> belt -> supply_depot -> frontline_supply_counter
```

The chain should produce at least one wartime output:

- ammo crates
- sandbag kits
- shell crates
- repair parts
- fuel canisters

Use simple recipe data, not hard-coded spaghetti.

---

## Visual target

The factory should look like a top-down 2.5D wartime production yard:

- muddy compacted industrial ground
- modular machines
- belts carrying crate/item tokens
- pipes and valves
- storage bins
- smoke and sparks
- muted military palette
- upper-left lighting
- readable silhouettes
- no high-detail hand-painted dependency

---

## Code quality rules

Use straightforward maintainable Unity code.

Prefer:

- ScriptableObject recipes
- data-driven machine definitions
- grid cell placement
- deterministic belt/item movement
- small modular components
- generated placeholder art if real art is missing
- clear editor tools

Avoid:

- physics-driven belt items
- complex pathfinding for initial belt logistics
- huge over-engineered simulation
- relying on imported asset packs
- manually placed fragile art dependencies

---

## Safety and preservation

Before changing code:

1. inspect the project structure
2. identify the active Unity version and existing folders
3. avoid deleting or overwriting unrelated work
4. place new systems under clearly named folders
5. preserve existing game systems unless they must be integrated

---

## Required report

At the end, write a short implementation report:

- files created
- files modified
- systems implemented
- vertical slice scene name
- known limitations
- next recommended tasks

The job is successful when the game has a working factory/logistics side that visually looks complete enough for a prototype and produces supply outputs that can feed the trench battlefield side.
