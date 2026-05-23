# Task 01 — Audit and Foundation

## Goal

Prepare the Unity project for the factory/logistics side without breaking existing work.

---

## Instructions for Codex

1. Inspect the existing Unity project structure.
2. Identify existing gameplay folders, art folders, scenes, prefabs, and scripts.
3. Do not delete existing battlefield/trench systems.
4. Create a clean factory-side folder structure if missing.
5. Add a short implementation note file describing what was found.

---

## Create folders

Create these if they do not already exist:

```text
Assets/TWB/Factory/
  Art/
    Source/
    Generated/
    Materials/
    Sprites/
    VFX/
    UI/
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
    Recipes/
    Buildings/
    Items/
  Scenes/
  Tests/
  Docs/
```

---

## Create project note

Create:

```text
Assets/TWB/Factory/Docs/factory_implementation_notes.md
```

Include:

- Unity version if identifiable
- existing relevant systems found
- new folders created
- no-overwrite decisions
- next task to run

---

## Acceptance criteria

This task is complete when:

- factory folders exist
- existing project systems are not broken
- implementation note exists
- Codex knows where future factory files should go
