# Vertical Slice Scene Implementation

## Purpose

Create one complete-looking scene proving the art direction works.

## Required scene

Create:

```text
Assets/TWB/Scenes/TWB_ArtPipeline_VerticalSlice.unity
```

## Scene goal

This scene is not the full game.

It is a visual proof that the game can look complete with the chosen art system.

## Required scene elements

### Camera

- orthographic camera
- top-down 2D composition
- size adjusted to show complete battlefield slice
- background color muted dark/earth tone if needed

### Terrain

- ground tile field
- mud variations
- trench floor network
- sandbag walls
- craters
- decals

### Trench network

Must include:

- horizontal trench section
- vertical trench section
- junction
- MG pocket
- mortar pocket
- supply path or approach

### Props

Place:

- ammo crates near MG/mortar
- planks/duckboards in trench
- barrels/fuel near logistics area
- debris and craters near front
- sandbag piles

### Weapons

Place:

- one MG emplacement
- one mortar emplacement
- optional bunker MG

### Units

Place:

- 2 riflemen
- 1 engineer
- 1 support gunner
- 1 truck
- 1 tank or armored support

At least some should animate or move in a small loop.

### VFX

Show:

- MG muzzle flash loop or timed fire
- mortar launch puff
- dirt impact
- smoke/fire near damage area
- dust near vehicle movement

### Factory/logistics area

Place a small rear area with:

- storage pallets
- industrial bin
- factory/module block or loading platform
- truck nearby
- supply crates

It should make the game feel like war logistics, not just a battlefield.

### UI/world overlays

Place:

- selection ring on one infantry
- move marker
- attack marker
- build ghost marker near logistics area

## Layout suggestion

Coordinate plan:

```text
x=-8..8, y=-5..5

Back/logistics area:
  x=-7..-3, y=-4..-1

Main trench:
  x=-6..6, y=0

Forward trench pocket:
  x=0, y=1..3

MG pocket:
  x=-4, y=1

Mortar pocket:
  x=3, y=-1

No man's land / crater area:
  x=-2..6, y=3..5
```

Codex may adjust layout as long as all elements are present.

## Object naming

Name objects clearly in the hierarchy:

```text
TWB_DemoSceneRoot
  Terrain
  Trenches
  Sandbags
  Decals
  Props
  Weapons
  Units
  VFX
  UIWorld
  LogisticsArea
```

## Scene lighting

If using SpriteRenderer only, lighting can be baked into sprites.

Do not require URP 2D lights unless the project already uses them.

## Demo behavior

Add simple scripts so the scene feels alive:

- one infantry patrol
- MG fires every few seconds
- mortar fires every few seconds
- smoke loops
- truck idles or moves slightly
- selection ring pulses

## Quality test

Scene passes if:

- user can screenshot it and it looks like a basic complete game
- trench is obvious
- sandbags are obvious
- MG and mortar are obvious
- units are readable
- VFX makes it feel alive
- logistics area is understandable
