# UI Icons and Overlays Implementation

## Purpose

Create enough UI art to make the prototype feel intentional and complete.

## Required generated UI assets

```text
Assets/TWB/Art/Generated/UI/ui_selection_ring_v001.png
Assets/TWB/Art/Generated/UI/ui_move_marker_v001.png
Assets/TWB/Art/Generated/UI/ui_attack_marker_v001.png
Assets/TWB/Art/Generated/UI/ui_build_ghost_v001.png

Assets/TWB/Art/Generated/UI/ui_icon_rifleman_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_engineer_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_mg_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_mortar_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_truck_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_tank_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_ammo_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_fuel_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_supplies_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_trench_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_factory_v001.png
Assets/TWB/Art/Generated/UI/ui_icon_repair_v001.png
```

## World overlays

### Selection ring

Size:

```text
128x128
```

Visual:

- thin military-style ring
- muted light blue/green or pale off-white
- transparent center
- subtle broken segments
- readable on mud/grass

### Move marker

Visual:

- small ring or arrow-like chevron
- muted blue/green
- not bright neon

### Attack marker

Visual:

- crosshair or target bracket
- muted red/orange
- transparent center

### Build ghost marker

Visual:

- transparent footprint rectangle/circle
- dotted or dashed border
- mild blue/green alpha
- should not look like final object

## Icons

Size:

```text
64x64
```

Visual:

- silhouette-first
- same muted panel/icon style
- small highlight and shadow
- transparent background
- clear at small size

## Icon construction recipes

### Rifleman icon

- helmet
- rifle silhouette
- small torso

### Engineer icon

- helmet
- wrench/tool shape
- small gear or pouch

### MG icon

- long barrel on tripod

### Mortar icon

- angled tube and base plate

### Truck icon

- top-down truck silhouette

### Tank icon

- top-down hull and turret

### Ammo icon

- ammo crate or shell

### Fuel icon

- jerry can or drum

### Supplies icon

- crate stack

### Trench icon

- zig-zag trench segment with sandbag edge

### Factory icon

- small industrial roof/stack silhouette

### Repair icon

- wrench and spark

## Optional panel art

Create a simple panel texture:

```text
Assets/TWB/Art/Generated/UI/ui_panel_field_dark_v001.png
```

Visual:

- dark muted metal/canvas
- subtle border
- slight edge wear
- no noisy center

## Runtime UI script

Create:

```text
Assets/TWB/Scripts/Runtime/UI/TwbPrototypeSelectionRing.cs
```

Behavior:

- pulsing alpha or scale
- optionally follows target transform
- can be used in demo scene

## Quality test

UI passes if:

- selection state is obvious
- icons are readable at 64x64
- UI style matches battlefield
- overlays do not look like debug primitives
