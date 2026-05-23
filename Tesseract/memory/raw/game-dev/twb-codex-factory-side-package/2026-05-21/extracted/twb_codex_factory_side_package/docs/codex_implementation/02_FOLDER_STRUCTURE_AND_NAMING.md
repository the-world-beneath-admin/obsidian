# Folder Structure and Naming

## Purpose

Define exactly where factory-side files should go.

---

## Preferred root

```text
Assets/TWB/Factory/
```

If the project already has a strong folder convention, use it while preserving this structure conceptually.

---

## Required folders

```text
Assets/TWB/Factory/Art/Generated/Floors
Assets/TWB/Factory/Art/Generated/Machines
Assets/TWB/Factory/Art/Generated/Belts
Assets/TWB/Factory/Art/Generated/Pipes
Assets/TWB/Factory/Art/Generated/Items
Assets/TWB/Factory/Art/Generated/VFX
Assets/TWB/Factory/Art/Generated/UI
Assets/TWB/Factory/Prefabs/Buildings
Assets/TWB/Factory/Prefabs/Belts
Assets/TWB/Factory/Prefabs/Pipes
Assets/TWB/Factory/Prefabs/Items
Assets/TWB/Factory/Prefabs/UI
Assets/TWB/Factory/Scripts/Core
Assets/TWB/Factory/Scripts/Grid
Assets/TWB/Factory/Scripts/Logistics
Assets/TWB/Factory/Scripts/Machines
Assets/TWB/Factory/Scripts/Recipes
Assets/TWB/Factory/Scripts/Visuals
Assets/TWB/Factory/Scripts/UI
Assets/TWB/Factory/Scripts/Editor
Assets/TWB/Factory/Data/Buildings
Assets/TWB/Factory/Data/Items
Assets/TWB/Factory/Data/Recipes
Assets/TWB/Factory/Scenes
Assets/TWB/Factory/Docs
```

---

## Script naming

Use clear class names.

Suggested names:

```text
FactoryGrid
FactoryGridCell
FactoryPlacementController
FactoryPlacementGhost
FactoryBuildingDefinition
FactoryPlacedObject
BeltSegment
FactoryItemToken
ItemDefinition
RecipeDefinition
MachineController
MachineInventory
MachinePort
StorageDepot
FrontlineSupplyDepot
FrontlineSupplyManager
FactoryPrototypeArtGenerator
FactoryBuildMenuUI
FactorySelectionPanelUI
```

---

## Asset naming

Use the naming rules from `docs/factory_pipeline/10_FILE_STRUCTURE_AND_EXPORT.md`.

---

## Completion criteria

This step is complete when the project has a predictable folder structure and future Codex tasks know exactly where files belong.
