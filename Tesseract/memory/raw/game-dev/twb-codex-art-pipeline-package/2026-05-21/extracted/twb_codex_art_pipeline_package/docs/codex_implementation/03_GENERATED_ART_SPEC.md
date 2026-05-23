# Generated Prototype Art Specification

## Purpose

Codex must create a first-pass art set programmatically.

The assets should be simple but cohesive.

## Visual technique

Use generated PNG textures with:

- muted colors
- simple shapes
- soft shadows
- top-left highlights
- bottom-right shadows
- controlled outlines
- small procedural noise
- simple texture marks
- transparent backgrounds for props/units/VFX/UI

## Supersampling

Where possible, draw at 2x or 4x resolution and downsample for anti-aliased edges.

Example:

- target sprite: 128x128
- draw buffer: 512x512
- downsample to 128x128

If supersampling is too much work, use simple alpha feathering around shapes.

## Palette

Recommended palette constants:

```text
ground_dark:     #4A3D2B
ground_mid:      #6B5A3B
ground_light:    #8A7750
mud_dark:        #2F261F
mud_mid:         #554334
mud_wet:         #1E1B18
trench_floor:    #3B3025
sandbag_base:    #8A7A52
sandbag_light:   #A49363
sandbag_shadow:  #5F5238
wood_base:       #6F4E32
wood_light:      #8B6845
metal_dark:      #2B2F2A
metal_mid:       #555E50
olive:           #4E5B36
olive_light:     #6D7A4B
canvas:          #766A4C
ui_dark:         #1E211C
ui_panel:        #2F332B
accent_blue:     #5E8CB8
accent_red:      #B05A4A
flash_yellow:    #FFD15A
smoke_gray:      #7B7B70
```

Codex may adjust slightly, but the palette must remain muted and consistent.

## Standard sprite sizes

### Terrain

- single terrain tile: 128x128
- trench tile: 128x128
- trench masks: 128x128
- larger node tile: 256x256

### Props

- small prop: 64x64
- medium prop: 128x128
- large prop: 256x256

### Weapons

- MG emplacement sheet: 256x128 or 512x128 depending frame count
- mortar emplacement sheet: 256x128 or 512x128

### Units

- infantry frame: 64x64
- infantry sheet: rows by directions/animations; width depends frame count
- vehicle frame: 128x128 or 192x192
- vehicle sheet: 4 directions x frames if used

### VFX

- small effect frame: 64x64
- explosion/smoke frame: 128x128
- sheets should use clean grid layout

### UI

- icon: 64x64
- selection ring: 128x128
- build ghost marker: 128x128

## Shape language

### Trenches

- dark compacted floor
- irregular but readable edge
- shadowed side lip
- optional plank/duckboard detail
- sandbag walls placed above the trench wall layer

### Sandbags

- chains of rounded capsules
- slightly varied sizes
- light top-left, dark bottom-right
- thin line detail / seam marks
- mud stains

### Machine gun

- long dark barrel
- compact receiver
- tripod or mount
- ammo box
- optional sandbag base
- tiny recoil frames

### Mortar

- round base plate
- angled tube shape in top-down readable form
- ammo shells/crate
- circular pit context if needed

### Infantry

- helmet circle/oval
- torso oval/rounded rectangle
- arms as simple forms
- rifle as dark thin rectangle
- feet/legs simple blobs
- faction accent stripe
- direction must be clear

### Vehicles

- top-down hull
- wheel/tread indications
- clear front/back
- turret/gun if tank
- dust/exhaust support

## Texture detail rules

Add only enough detail to avoid flatness:

- 2 to 5 scratches on wood
- few speckles on dirt
- few scuffs on metal
- simple stitches/seams on sandbags
- small shadow under props

Do not add noise so strong that silhouettes become unclear.

## Alpha rules

Transparent sprites should have clean edges and no matte background.

If edge pixels are semi-transparent, make sure they blend against muddy terrain.

## Readability test

Every generated asset should pass:

1. View at 100%.
2. View at 50%.
3. View in demo scene.
4. Ask: can a player tell what it is in one second?

If not, simplify silhouette or increase contrast.
