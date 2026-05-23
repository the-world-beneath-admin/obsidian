# Unit Animation System

## Purpose

Create simple readable units and animations.

The first pass should use tiny helmeted soldiers with guns, not complex realistic human sprites.

## Core scripts

Create:

```text
Assets/TWB/Scripts/Runtime/Art/TwbSimpleSpriteAnimator.cs
Assets/TWB/Scripts/Runtime/Units/TwbPrototypeUnitMotor.cs
Assets/TWB/Scripts/Editor/ArtPipeline/TwbAnimationBuilder.cs
```

## Unit prefabs

Create:

```text
Assets/TWB/Prefabs/Units/TWB_Unit_Rifleman.prefab
Assets/TWB/Prefabs/Units/TWB_Unit_Engineer.prefab
Assets/TWB/Prefabs/Units/TWB_Unit_SupportGunner.prefab
Assets/TWB/Prefabs/Units/TWB_Unit_SupplyTruck.prefab
Assets/TWB/Prefabs/Units/TWB_Unit_Tank.prefab
```

## Infantry frame design

Frame size:

```text
64x64
```

Visual layout:

- helmet centered near upper half
- torso below helmet
- arms/gun shape extending directionally
- tiny legs/feet
- faction accent stripe/mark
- top-left highlight
- small contact shadow

## Directions

Generate frames for:

```text
down
up
left
right
```

If diagonal movement exists in game, map diagonals to closest 4-direction frame for now.

## States

Generate frames for:

```text
idle
move
fire
```

### Idle

- 2 frames
- subtle breathing/bob
- weapon stable

### Move

- 4 frames
- simple leg alternation
- slight torso bob

### Fire

- 3 frames
- aiming frame
- recoil frame
- return frame

## Infantry roles

### Rifleman

- standard rifle
- balanced silhouette
- default helmet/body

### Engineer

- backpack/tool pouch
- shorter weapon or tool shape
- slightly different accent

### Support gunner

- heavier weapon silhouette
- bulkier body or ammo pack
- longer firing barrel

## Vehicle frame design

### Supply truck

Frame size:

```text
128x128
```

Visual:

- top-down cab and bed
- visible wheels
- supply crate marks in bed
- clear front
- faction mark

States:

- idle: 1 frame per direction
- move: 2 frames per direction or simple wheel/dust effect

### Tank

Frame size:

```text
128x128
```

Visual:

- top-down hull
- turret/gun
- treads
- clear front
- muted olive color

States:

- idle: 1 frame per direction
- move: optional 2 frames
- fire: optional recoil/turret frame

## TwbSimpleSpriteAnimator

This runtime script should:

- hold named animation clips or arrays of sprites
- switch animation by state string or enum
- play frames at configurable FPS
- optionally loop or one-shot
- expose `Play(string animationName)`

Keep it simple.

Do not build a complex animation controller unless the project already has one.

## TwbPrototypeUnitMotor

For the demo scene only, this script can:

- move unit along a small looping path
- face movement direction
- switch between idle and move
- occasionally trigger fire animation
- optionally spawn muzzle flash

This proves the art works even before full gameplay integration.

## Animation clip option

If Unity AnimationClips are easier, Codex can create them in editor and attach Animator components.

However, a simple sprite-array animator is usually more stable for generated prototype sprites.

## Quality test

Units pass if:

- helmet is visible
- weapon is visible
- direction is clear
- idle/move/fire are distinguishable
- role is readable enough at gameplay zoom
- units do not look like random blobs
