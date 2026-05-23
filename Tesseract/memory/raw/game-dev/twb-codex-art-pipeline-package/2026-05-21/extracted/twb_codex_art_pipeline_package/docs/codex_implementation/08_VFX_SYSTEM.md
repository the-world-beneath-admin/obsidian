# VFX System Implementation

## Purpose

Create simple reusable VFX that make the basic art feel alive.

## Core scripts

Create:

```text
Assets/TWB/Scripts/Runtime/VFX/TwbOneShotVfx.cs
Assets/TWB/Scripts/Runtime/VFX/TwbLoopingVfx.cs
```

Optional:

```text
Assets/TWB/Scripts/Editor/ArtPipeline/TwbVfxPrefabBuilder.cs
```

or include VFX creation in `TwbPrefabBuilder`.

## VFX prefabs

Create:

```text
Assets/TWB/Prefabs/VFX/TWB_VFX_RifleMuzzleFlash.prefab
Assets/TWB/Prefabs/VFX/TWB_VFX_MGMuzzleFlash.prefab
Assets/TWB/Prefabs/VFX/TWB_VFX_MortarLaunchPuff.prefab
Assets/TWB/Prefabs/VFX/TWB_VFX_DirtImpact.prefab
Assets/TWB/Prefabs/VFX/TWB_VFX_SmallExplosion.prefab
Assets/TWB/Prefabs/VFX/TWB_VFX_SmokeLoop.prefab
Assets/TWB/Prefabs/VFX/TWB_VFX_FireLoop.prefab
Assets/TWB/Prefabs/VFX/TWB_VFX_DustPuff.prefab
```

## VFX generation

### Muzzle flash

Frame size:

```text
64x64
```

Frame count:

```text
3 to 5
```

Visual:

- yellow/orange compact flash
- slight white-hot center
- transparent background
- quick fade
- not huge

### MG muzzle flash

Similar to rifle but slightly wider/brighter.

### Mortar launch puff

Frame size:

```text
128x128
```

Frame count:

```text
4 to 6
```

Visual:

- gray/brown smoke puff at base
- expanding soft circles
- transparent fade
- no giant explosion

### Dirt impact

Frame size:

```text
128x128
```

Frame count:

```text
4 to 6
```

Visual:

- brown dirt burst
- small particles
- brief smoke/dust

### Small explosion

Frame size:

```text
128x128
```

Frame count:

```text
5 to 8
```

Visual:

- quick flash
- orange/brown core
- expanding smoke
- dirt fragments

### Smoke loop

Frame size:

```text
128x128
```

Frame count:

```text
6 to 8
```

Visual:

- soft gray smoke blobs
- slightly changing shape
- loop should not pop badly

### Fire loop

Frame size:

```text
128x128
```

Frame count:

```text
4 to 6
```

Visual:

- small battlefield flame
- orange/yellow core
- transparent edges
- optional smoke on top

### Dust puff

Frame size:

```text
64x64
```

Frame count:

```text
3 to 5
```

Visual:

- tan/gray puffs
- for movement and vehicle dust

## TwbOneShotVfx

Runtime behavior:

- plays a sprite frame sequence once
- destroys or disables itself after completion
- configurable FPS
- optional scale fade
- optional alpha fade

## TwbLoopingVfx

Runtime behavior:

- loops sprite frames
- configurable FPS
- optional random start frame
- optional gentle scale/alpha variation

## Spawn points

Weapon prefabs should include anchors:

```text
MuzzleAnchor
LaunchAnchor
ImpactAnchor
SmokeAnchor
```

## Demo scene VFX showcase

The demo scene should show:

- MG firing loop using muzzle flash
- mortar launch puff occasionally
- dirt impact loop or timed example
- smoke/fire near destroyed object or crater
- dust puff near vehicle path

## Quality test

VFX pass if:

- fire events are visible
- combat feels active
- effects do not obscure the whole map
- effects match muted battlefield style
- simple units feel more alive because of effects
