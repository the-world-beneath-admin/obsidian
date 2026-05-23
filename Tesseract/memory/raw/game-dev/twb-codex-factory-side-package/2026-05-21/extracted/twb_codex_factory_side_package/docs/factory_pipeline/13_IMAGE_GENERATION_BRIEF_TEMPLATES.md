# Image Generation Brief Templates

## Purpose

These templates describe how to request source art if image generation is used.

Codex should still support generated placeholder art through code.
Image generation should improve source assets, not block development.

---

## 1. General rules

Every factory-side image request should specify:

- top-down orthographic view
- stylized tactical wartime factory look
- modular reusable asset
- transparent or clean background
- upper-left lighting
- readable at game zoom
- not a full scene unless specifically requested
- no text labels unless UI icons require symbol design
- do not copy an existing game's art style exactly

---

## 2. Factory floor material sheet

Create a square top-down orthographic material source sheet for a stylized wartime factory/logistics game.

Include reusable separated material zones for:

- compacted dirt industrial yard
- worn concrete pad
- muddy edge
- metal plate floor
- loading pad surface
- oil stain patch
- tire mark patch
- scrap/debris patch

Style:

- muted military-industrial palette
- readable at gameplay zoom
- upper-left lighting
- no labels
- no full scene perspective
- no photorealism

---

## 3. Conveyor belt asset sheet

Create a top-down isolated conveyor belt asset sheet for a stylized tactical factory game.

Include:

- straight horizontal belt segment
- straight vertical belt segment
- four corner belt segments
- optional input/output cap

Requirements:

- dark belt surface
- simple side rails
- clear direction cue
- consistent tile size
- transparent background
- upper-left lighting
- readable on muddy floor

---

## 4. Pipe asset sheet

Create a top-down isolated pipe asset sheet for a stylized wartime factory game.

Include:

- straight horizontal pipe
- straight vertical pipe
- four elbow corners
- valve piece
- pump connector if possible

Requirements:

- dull metal material
- simple flanges
- top-down readability
- transparent background
- no full scene

---

## 5. Machine asset template

Create a top-down isolated machine sprite for a stylized wartime factory/logistics game.

Machine type:
`[extractor / processor / workshop / depot / generator]`

Requirements:

- clear silhouette for machine role
- compact utilitarian military-industrial design
- visible input/output side if applicable
- upper-left lighting
- contact shadow if useful
- transparent background
- no crew characters
- no full factory scene
- readable at game zoom

---

## 6. Item icon/token sheet

Create a small item icon/token sheet for a stylized wartime factory game.

Include icons for:

- ore chunk
- metal parts
- ammo crate
- sandbag kit
- fuel can
- repair parts
- shell crate

Requirements:

- readable as UI icons and belt tokens
- simple silhouettes
- transparent background
- consistent lighting and palette
- not tiny realistic detail

---

## 7. VFX sheet

Create a small game-ready VFX sprite sheet for a stylized wartime factory game.

Effect type:
`[smoke puff / spark flicker / dust puff / output pulse / steam puff]`

Requirements:

- transparent background
- isolated frames
- low frame count
- readable but not overpowering
- muted battlefield-industrial style

---

## 8. UI status icon sheet

Create clean UI status icons for a stylized wartime factory game.

Include:

- working
- missing input
- output blocked
- no power
- storage full
- recipe active

Requirements:

- simple shape-first icons
- readable at small size
- transparent background
- consistent stroke/shading
- practical military UI feel

---

## 9. Rule for Codex

Codex must not ask for one giant image containing the whole factory.

Request one asset family at a time.
Use code and modular assembly to build the final game scene.
