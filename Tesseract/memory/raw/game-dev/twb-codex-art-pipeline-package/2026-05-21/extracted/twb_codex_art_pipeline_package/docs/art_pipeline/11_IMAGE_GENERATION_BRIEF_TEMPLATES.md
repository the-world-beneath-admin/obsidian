# Image Generation Brief Templates

## Purpose

This document gives Codex the prompt structure to use when requesting source art, if image generation is available.

These are not final consumer prompts.
These are structured production prompts.

Codex should adapt them per asset family.

If image generation is not available in the current Codex environment, Codex must still proceed by generating simple procedural Unity art from the implementation docs.

## 1. General prompt rules

Every image-generation brief should specify:

- subject type
- intended use
- camera/view
- style
- background / alpha expectations
- what must be included
- what must be excluded
- modularity requirement
- readability target

### Mandatory wording themes

- top-down or orthographic
- readable at gameplay scale
- modular or reusable
- not a full scene unless explicitly needed
- consistent upper-left lighting
- stylized military tactical game art
- not photorealistic
- not perspective-heavy

## 2. Terrain material sheet template

Create one square top-down orthographic material source sheet for a stylized tactical trench warfare game.

This is a source sheet only, not a gameplay screenshot, not a full map, and not a tile sheet with labels.

Include reusable separated material zones for:

- outer ground soil
- trench floor
- wet mud variant
- sandbag material
- timber reinforcement
- debris / rubble patch
- darker worn mud patch

Visual style:

- stylized but believable battlefield materials
- readable at game zoom
- muted military palette
- upper-left lighting
- no hard outlines
- no perspective scene
- no text or labels

## 3. Trench mask template

Create a square top-down trench mask image for a modular trench system in a tactical game.

This is a mask asset, not a full colored sprite.

Asset type:

`[insert exact piece: straight horizontal / corner outer / t-junction / etc.]`

Requirements:

- clear centered trench form
- tile-safe or modular edge design as appropriate
- black background
- white mask shape for the trench or wall footprint
- readable and clean silhouette
- no shading unless this is specifically a shadow mask
- slight organic irregularity is acceptable if it stays modular

## 4. Sandbag overlay template

Create a top-down isolated sandbag trench overlay asset for a stylized tactical war game.

Asset type:

`[straight strip / corner / cap / arc segment]`

Requirements:

- readable lumpy connected sandbags
- field-built imperfect shape
- muted khaki / olive military palette
- upper-left lighting
- transparent or clean extraction-friendly background
- no surrounding environment
- modular, reusable, and scale-consistent
- clear top-down readable sandbag segmentation
- not photorealistic
- not a full trench scene

## 5. Prop template

Create a top-down isolated battlefield prop sheet for a stylized tactical trench warfare game.

Include:

`[list exact props]`

Requirements:

- isolated assets
- transparent or clean matte background
- consistent scale
- top-down orthographic view
- stylized readable military objects
- slightly worn / used
- not hyper-detailed
- no full scene

## 6. Weapon emplacement template

Create a top-down isolated `[machine gun emplacement / mortar emplacement]` for a stylized tactical trench warfare game.

Requirements:

- strong readable silhouette
- clear identification of the weapon role
- slight 2.5D readability but still top-down
- transparent or clean matte background
- upper-left lighting
- field-worn military materials
- optional nearby ammo/support prop if it helps readability
- no crew unless explicitly requested
- not a full battlefield scene

## 7. Unit sprite sheet template

Create a sprite sheet for a small top-down infantry unit for a stylized tactical trench warfare game.

Unit type:

`[rifleman / engineer / support gunner]`

Requirements:

- tiny military miniature style
- visible helmet
- visible gun silhouette
- simplified hands and anatomy
- no facial detail needed
- readable at gameplay scale
- 4 directions
- `[idle / move / fire]` animation rows as requested
- consistent frame size and alignment
- transparent background
- muted military palette
- not photorealistic
- not large character art

## 8. VFX template

Create a small top-down or game-ready particle effect sheet for a stylized tactical battlefield game.

Effect type:

`[muzzle flash / smoke / dirt impact / explosion / dust puff]`

Requirements:

- readable at gameplay scale
- isolated frames
- transparent background
- consistent styling
- supports low-frame-count animation
- not overly realistic
- not neon
- suitable for military battlefield action

## 9. UI icon template

Create a set of clean game UI icons for a stylized military trench warfare game.

Include:

`[list exact icons]`

Requirements:

- simple silhouette-first icons
- readable at small size
- consistent style
- practical military theme
- limited detail
- transparent background
- no decorative scene background

## 10. Codex usage rule

Codex should never request “make everything in one image.”

Codex should request:

- one family at a time
- one asset purpose at a time
- source-first outputs
- modular outputs
- game-usable outputs
