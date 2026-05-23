# Visual Recipe Details

## Purpose

This file gives concrete procedural drawing recipes.

Codex can use these recipes to create prototype art without needing a human artist.

## General rendering recipe

For each sprite:

1. create transparent texture
2. draw soft shadow under object
3. draw base silhouette
4. draw top-left highlight
5. draw bottom-right shade
6. draw 2 to 8 small detail marks
7. draw outline or crease lines only where readability needs it
8. save PNG
9. import as sprite

## Sandbag strip

### Horizontal strip

- sprite size: 128x128
- draw 5 to 7 rounded capsules across center
- each bag overlaps slightly
- color varies slightly per bag
- highlight top-left edge
- darker crease line between bags
- small mud speckles near lower edge
- shadow below strip

### Vertical strip

Same as horizontal but arranged vertically.

### Corners

- arrange capsules in an L shape
- ensure clear corner mass
- avoid gaps

## Trench tile

- sprite size: 128x128
- draw irregular dark trench floor band
- add darker inner shadow on one side
- add lighter loose dirt edge
- add subtle footprints/scuffs
- place sandbag overlay separately when possible

## Crater

- transparent sprite
- draw large dark soft oval
- draw uneven rim with brown highlights
- add small fragments around rim
- add darker center
- optional scorch speckles

## Ammo crate

- sprite size: 64x64 or 128x128
- draw top-down rectangle
- color: dull olive/brown
- darker side/shadow
- thin plank lines
- small ammo stripe or shell mark
- contact shadow

## Fuel drum

- sprite size: 64x64
- draw top-down cylinder/ellipse
- dark olive/gray
- ring bands
- small cap highlight
- contact shadow

## Machine gun

- sprite size: 128x128
- draw sandbag base or tripod
- draw receiver block
- draw long thin barrel toward front
- draw ammo box to side
- draw dark metal and olive tones
- firing frames shift barrel/receiver backward by 2 to 4 pixels
- muzzle anchor at barrel tip

## Mortar

- sprite size: 128x128
- draw circular base plate
- draw tube as short dark angled/vertical shape
- draw support legs
- draw shell crate
- fire frames lower/recoil tube slightly
- launch puff at tube/base area

## Rifleman

- sprite size: 64x64
- body should occupy roughly center 28x36 px
- helmet: oval/circle
- torso: rounded rectangle/oval
- rifle: dark thin shape extending direction
- legs: two small dark shapes
- faction accent: tiny stripe or shoulder patch
- no facial details required

## Engineer

Same as rifleman but add:

- small backpack/tool pouch
- tool shape or shorter weapon
- alternate accent color

## Support gunner

Same as rifleman but add:

- longer heavier weapon
- larger ammo pack
- slightly bulkier torso

## Truck

- sprite size: 128x128
- draw rectangular bed
- cab front
- wheels as dark side circles/rectangles
- crates in bed
- clear front direction
- small faction mark

## Tank

- sprite size: 128x128
- draw oval/rounded rectangular hull
- treads along sides
- turret in center
- gun barrel toward front
- hatch/detail lines
- clear front direction

## Muzzle flash

- transparent sprite
- draw 3 to 5 triangular/oval flame shapes
- white/yellow center
- orange outer
- fade quickly across frames

## Smoke

- transparent sprite
- draw overlapping soft circles
- gray/brown palette
- grow and fade over frames
- randomize starting frames for loops

## UI icons

- 64x64
- dark transparent or no background
- silhouette centered
- simple highlight and shadow
- consistent stroke thickness
- no tiny details that vanish
