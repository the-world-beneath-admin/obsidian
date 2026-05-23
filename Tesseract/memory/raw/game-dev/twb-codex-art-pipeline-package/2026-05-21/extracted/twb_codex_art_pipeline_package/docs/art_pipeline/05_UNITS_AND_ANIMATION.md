# Units and Animation

## Purpose

This document defines how unit art should work.

The unit system must be scalable and cheap to produce.

That means:

- small sprites
- low frame counts
- clear silhouettes
- few directions
- effect-assisted motion

## 1. Unit philosophy

The game does not need detailed soldiers.

It needs:

- clearly military units
- visible helmets
- visible guns
- visible motion
- readable faction markers

### Final decision

Use:

- helmets
- guns
- simplified hands or arms
- tiny readable military bodies

Do not chase detailed anatomy.

## 2. Unit categories

### Infantry

- rifleman
- engineer
- machine gunner / support gunner
- mortar crew
- officer / commander
- medic optional
- logistics carrier / worker

### Vehicles

- supply truck
- light transport
- tank
- artillery tractor
- scout car if needed

### Crew-served support

- MG team
- mortar team
- artillery crew

These may be separate unit sprites plus emplacement sprites.

## 3. Infantry visual design rules

### Silhouette components

Each infantry sprite should have:

- helmet
- torso
- legs
- gun silhouette
- optional backpack
- optional shoulder pack or tool bag
- faction armband, stripe, or gear accent

### Simplification rules

- face detail minimal or omitted
- hands implied if needed
- feet simple
- body slightly chunky for readability
- avoid thin realistic proportions

### Gameplay readability priorities

1. direction
2. weapon type
3. state
4. faction
5. specialty role

## 4. Role differentiation

### Rifleman

- standard rifle silhouette
- balanced posture
- default infantry look

### Engineer

- tool pouch or backpack
- shorter carbine or tool in off hand
- utility look

### Machine gunner

- heavier weapon silhouette
- ammo pack or heavier posture
- possibly slower stance

### Mortar crew

- can be regular infantry plus mortar emplacement
- carry shell or support gear if enough room

### Officer

- slightly distinct posture
- binoculars, sidearm, or command marker
- not too flashy

### Logistics worker

- crate carry pose, satchel, or work gear
- useful for factory/supply scenes

## 5. Vehicle rules

Vehicles are easier than people and should carry more visual weight where possible.

### Vehicle categories

- truck
- half-track if desired
- tank
- light utility tractor
- artillery tow vehicle

### Visual treatment

- top-down readable hull
- clear turret if present
- visible wheel or tread indication
- faction marking
- dust/smoke support via particles

### Simplification

- avoid dense rivet detail
- shape and function matter most

## 6. Direction rules

### Infantry

Recommended:

- 4-direction production first
- up
- down
- left
- right

Optional later:

- diagonal blends or 8-direction expansion

### Vehicles

- 4 directions or rotational code support
- turret rotation done separately if possible

### Emplacements

- often do not need true directional sets if rotation can be handled in-engine

## 7. Animation set rules

Keep frame counts low and focused.

### Infantry minimum viable set

- idle: 2 to 4 frames
- move: 4 to 6 frames
- fire: 2 to 4 frames
- death: optional, 2 to 4 frames
- special action: optional, engineer place/use motion

### Vehicle minimum viable set

- idle: 1 to 2 frames
- move: 2 to 4 frames or simple body bob
- fire: 2 to 3 frames
- destroyed state: static wreck sprite

### Emplacement minimum viable set

- idle: 1 frame
- fire: 2 to 4 frames recoil cycle
- destroyed/damaged: static variant

## 8. Motion style

Animation should be readable, not realistic.

### Infantry move

- short step cycle
- slight body bob
- weapon held consistently

### Infantry fire

- small recoil
- muzzle flash does most of the work

### Vehicle move

- slight bounce
- track/wheel implication
- dust puff support

### MG fire

- barrel/body recoil
- flash
- shell ejection optional

### Mortar fire

- puff/smoke burst
- brief recoil
- shell departure implied more by VFX than sprite frame detail

## 9. Sprite sheet strategy

Codex should generate units as organized sheets, not random loose frames.

### Sheet structure per unit

- row per direction
- columns per animation frame
- clean consistent padding
- transparent background
- same bounding box per row

### Example groups

- `unit_rifleman_sheet_v001.png`
- `unit_engineer_sheet_v001.png`
- `unit_support_gunner_sheet_v001.png`
- `unit_supply_truck_sheet_v001.png`
- `unit_tank_sheet_v001.png`

## 10. Faction differentiation

Do not generate wholly unique anatomy and costume sets for every side unless needed.

Use:

- helmet color accents
- shoulder patches
- gear color variation
- vehicle marking symbols
- banner or UI overlay support

This keeps the workload manageable.

## 11. What units should look like

At gameplay zoom, units should read as:

- tiny military miniatures
- easy to understand
- moving with purpose
- matching the battlefield tone

If they are small, solid, and readable, they are successful.

That is better than ambitious bad character art.
