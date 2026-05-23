# Codex Task 04 — Build Props, Weapons, and Units

Read:

- `docs/art_pipeline/04_PROPS_AND_WEAPONS.md`
- `docs/art_pipeline/05_UNITS_AND_ANIMATION.md`
- `docs/codex_implementation/06_PROP_WEAPON_PREFABS.md`
- `docs/codex_implementation/07_UNIT_ANIMATION_SYSTEM.md`

## Task

Create prefabs and simple animation systems for battlefield props, weapons, and units.

## Requirements

Create:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrefabBuilder.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbAnimationBuilder.cs
Assets/TWB/Scripts/Runtime/Art/TwbSimpleSpriteAnimator.cs
Assets/TWB/Scripts/Runtime/Units/TwbPrototypeUnitMotor.cs
Assets/TWB/Scripts/Runtime/Weapons/TwbPrototypeWeaponAnimator.cs
```

Create prefabs:

- ammo crate
- supply crate
- fuel drum
- barrel
- plank bundle
- sandbag pile
- wire spool
- shell box
- MG emplacement
- mortar emplacement
- bunker MG
- rifleman
- engineer
- support gunner
- supply truck
- tank

## Animation

- infantry: idle/move/fire
- MG: idle/fire recoil
- mortar: idle/fire recoil
- vehicle: idle/move or simple demo motion

## Done when

- prefabs exist
- units visibly look like helmeted soldiers with guns
- MG and mortar are identifiable
- demo scripts can animate units/weapons
