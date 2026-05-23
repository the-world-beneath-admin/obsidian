# Props and Weapon Prefabs

## Purpose

Create prefabs for battlefield props and weapon emplacements.

## Core scripts

Create or update:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbPrefabBuilder.cs
Assets/TWB/Scripts/Runtime/Weapons/TwbPrototypeWeaponAnimator.cs
```

## Prefab structure

Each prefab should be simple:

```text
PrefabRoot
  SpriteRenderer
  OptionalShadowSprite
  OptionalVfxAnchor
  OptionalScript
```

Use child objects for:

- muzzle anchor
- smoke anchor
- projectile origin
- selection marker anchor
- shadow sprite if needed

## Prop prefabs

Create:

```text
Assets/TWB/Prefabs/Props/TWB_Prop_AmmoCrate.prefab
Assets/TWB/Prefabs/Props/TWB_Prop_SupplyCrate.prefab
Assets/TWB/Prefabs/Props/TWB_Prop_FuelDrum.prefab
Assets/TWB/Prefabs/Props/TWB_Prop_Barrel.prefab
Assets/TWB/Prefabs/Props/TWB_Prop_PlankBundle.prefab
Assets/TWB/Prefabs/Props/TWB_Prop_SandbagPile.prefab
Assets/TWB/Prefabs/Props/TWB_Prop_WireSpool.prefab
Assets/TWB/Prefabs/Props/TWB_Prop_ShellBox.prefab
```

## Weapon prefabs

Create:

```text
Assets/TWB/Prefabs/Weapons/TWB_Weapon_MGEmplacement.prefab
Assets/TWB/Prefabs/Weapons/TWB_Weapon_MortarEmplacement.prefab
Assets/TWB/Prefabs/Weapons/TWB_Weapon_BunkerMG.prefab
```

## Machine gun prefab

### Visual structure

```text
TWB_Weapon_MGEmplacement
  BodySprite
  MuzzleAnchor
  OptionalAmmoBox
  OptionalSandbagBase
```

### Sprite requirements

- idle frame
- fire recoil frame 0
- fire recoil frame 1

### Animation

The firing cycle should be short:

1. idle
2. flash spawn
3. recoil frame
4. return frame
5. idle

### Readability

Must clearly show:

- barrel
- firing direction
- defensive role

## Mortar prefab

### Visual structure

```text
TWB_Weapon_MortarEmplacement
  BodySprite
  LaunchAnchor
  OptionalAmmoCrate
  OptionalPitShadow
```

### Sprite requirements

- idle frame
- launch/recoil frame
- return frame

### Animation

Mortar launch should use:

- sprite recoil
- smoke puff
- optional shell arc indicator in demo only

### Readability

Must clearly show:

- base plate / pit
- mortar tube
- indirect-fire identity

## Bunker MG prefab

A simple low bunker or firing slit.

Visual:

- squat reinforced position
- firing slit
- small gun barrel
- sandbag/earth cover

This can be static for the first pass.

## Prop quality rules

Props should include:

- small shadow under asset
- top-left highlight
- muted palette
- simple detail marks
- clear silhouette

## Collider rules

For prototype prefabs, add simple colliders only if helpful:

- `BoxCollider2D` for crates/buildings
- `CircleCollider2D` for barrels
- no collider for pure decals

Avoid complex physics unless required by existing gameplay.

## Integration

If existing gameplay systems expect components, Codex may add adapters to prefabs, but should not break existing architecture.

Document all assumptions in the report.
