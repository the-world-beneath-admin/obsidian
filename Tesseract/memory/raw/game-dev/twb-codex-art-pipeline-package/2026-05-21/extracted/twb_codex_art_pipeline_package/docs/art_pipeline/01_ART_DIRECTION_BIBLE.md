# Art Direction Bible

## Purpose

This document defines what the game should look like.

It is the source of truth for:

- visual style
- camera assumptions
- scale
- silhouette language
- material treatment
- lighting
- color
- readability
- detail limits

Codex must follow this document when generating or assembling art.

## 1. Game visual identity

The game is a top-down war / logistics / trench simulation with a slight 2.5D feel.

The visual tone should communicate:

- battlefield function
- military readability
- muddy trench warfare
- practical equipment
- organized logistical support
- controlled chaos
- a game that feels complete even when simplified

The world should feel like a small tactical diorama rather than a realistic film set.

## 2. Camera assumptions

### Camera type

- top-down orthographic or near-orthographic
- slight readability tilt is acceptable only if very mild
- no strong perspective

### View angle

- primarily top-down
- objects may imply height using top surfaces, side lips, and shadows
- do not create side-view art

### Gameplay readability

The player must be able to immediately read:

- traversable ground
- trench boundaries
- sandbag walls
- emplacements
- cover objects
- buildings
- factories
- supply objects
- units
- projectiles / VFX

## 3. Style pillars

### Pillar A: Readable

The first job of every asset is to be readable from gameplay height.

### Pillar B: Consistent

All assets must feel like they belong to the same world.

### Pillar C: Modular

Assets should be made from reusable components whenever possible.

### Pillar D: Efficient

The asset system must be reproducible by Codex at scale.

### Pillar E: Complete

The total presentation should feel like a finished game, even if individual assets are simple.

## 4. Visual simplification level

Target a simplification level between:

- realistic enough to identify military gear
- stylized enough to be maintainable

### Good examples of simplification

- infantry: tiny helmeted figures with gun silhouette, not detailed anatomy
- sandbags: clearly segmented lumpy rows, not hyper-detailed fabric simulation
- machine guns: recognizable tripod/gun silhouette, not exact real-world engineering
- mortar: round base plate + tube + ammo crates
- bunkers: compact reinforced shape with obvious firing slit or roof
- factories: simple industrial forms with pipes, vents, stacks, conveyor cues

### Bad examples

- complex human faces
- realistic cloth folds on tiny units
- excessive surface noise
- decorative detail that destroys readability
- perspective-heavy painted scenes
- exaggerated comic outlines inconsistent with the rest of the assets

## 5. Color direction

### Overall palette

- muted battlefield colors
- earth tones dominate
- faction colors are used as accents
- VFX may use brighter contrast

### Terrain palette

- mud browns
- soil tan / gray-brown
- olive greens
- desaturated vegetation
- damp dark patches
- timber browns
- dusty khakis

### Military object palette

- olive drab
- khaki
- gray metal
- brown wood
- dark rubber / black components
- red-brown rust accents only when controlled

### Accent colors

Use sparingly for:

- faction identity
- selected units
- command indicators
- interactive factory components
- UI states

### Avoid

- neon military assets
- oversaturated cartoon colors
- glossy plastic look unless a specific device needs it

## 6. Lighting model

### Primary light

- upper-left directional light

### Asset lighting assumptions

- top surfaces slightly brighter
- lower-right side slightly darker
- contact shadow under props
- trench inner lip darker than surrounding ground
- shadow overlays should be simple and readable

### Avoid

- dramatic cinematic shadows
- multiple inconsistent light sources
- harsh black shadow pools
- shiny specular highlights except for small wet accents

## 7. Surface treatment

### Materials should look:

- used
- field-worn
- practical
- readable
- not dirty beyond recognition

### Sandbags

- clearly lumpy
- field-made
- worn but functional
- visible seams and tied ends in simplified form
- slight dirt and stains

### Mud

- compacted
- low contrast
- subtle scuffs
- not mirror-wet

### Wood

- rough
- functional
- split grain or planks visible
- slightly muddy or weathered

### Metal

- matte
- military-grade
- slight wear
- limited rust

## 8. Silhouette language

Silhouette clarity is more important than texture detail.

### Desired silhouettes

- trenches: clear channels with edge definition
- sandbags: rounded linked forms
- machine guns: long forward barrel on stable support
- mortars: upward tube with circular pit context
- crates: clean rectangular shapes
- bunkers: low squat reinforced shapes
- infantry: helmet + torso + weapon silhouette
- vehicles: broad top shape and gun/body identity

### Silhouette test

If an asset is shrunk small and still readable, it passes.

## 9. Unit scale philosophy

Units should be small enough that:

- animation requirements stay manageable
- identity comes from helmet/weapon posture/faction color
- lack of facial detail is not a problem

### Unit representation

Infantry should be:

- tiny helmeted military miniatures
- visible gun silhouette
- visible hands only if they help readability
- visible face detail not required
- proportions slightly chunky for readability

This means:

**Use helmets with guns. Hands can be simplified. Faces can be nearly absent.**

## 10. Animation philosophy

Use few frames, strong silhouettes, and good effects.

### Infantry

- idle
- move
- fire
- death / collapse optional depending on scope

### Emplacements

- idle
- firing recoil
- reload pose optional

### Vehicles

- idle
- move treads/wheels implied
- turret fire if applicable

### Effects do heavy lifting

The animation will feel better through:

- muzzle flashes
- dust puffs
- smoke
- shell trails
- impact bursts
- recoil motion
- timing polish

## 11. What “complete” should look like

A scene should feel complete because it has:

- solid terrain materials
- clear trench layout
- sandbag cover
- guns and props
- believable emplacements
- small moving units
- smoke and fire effects
- clear UI overlays
- consistent shading and palette

Perfection is not required.
Consistency is required.

## 12. Final visual sentence

The game should look like a **clean, readable, stylized battlefield miniature simulation with believable trenches, military props, simple soldiers, and functional wartime industry.**
