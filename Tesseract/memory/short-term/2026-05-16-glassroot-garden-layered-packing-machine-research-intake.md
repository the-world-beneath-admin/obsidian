# 2026-05-16 Glassroot Garden Layered Packing Machine Research Intake

## Task

Intake user-provided research about efficient layered animation for multi-part automated machines, then apply it to the Glassroot Garden herb drying room packing/bundling machine plan.

Scope: Glassroot Garden World Key.

## Source

User-provided research titled:

`WW1 Steampunk/Magitech Mine - Layered Animation Breakdown`

The research used a mine as the example, but the durable design principle applies to the Garden packing machine: do not animate the entire machine as one large sprite sheet when small child layers, transform animation, particles, glow overlays, and limited sprite swaps can produce a richer result more efficiently.

## Core Research Intake

The important principle is:

Static painted machine body
+ small animated machine parts
+ transform rotation/movement
+ particles
+ glow overlays
+ state-based effects

This gives a machine visual complexity without wasting texture memory on a huge full-machine frame strip.

## Translation To Glassroot Garden

The original research speaks in Unity prefab terms. Glassroot Garden is Phaser/TypeScript, so the implementation should translate as:

- Unity child SpriteRenderers -> Phaser images/sprites grouped by container/depth.
- Unity transform movement -> Phaser tweens.
- Unity rotation -> Phaser rotation tweens.
- Unity alpha pulse -> Phaser alpha tweens.
- Unity particle systems -> Phaser particles.
- Sprite swaps -> Phaser texture/frame swaps or replacing a small image.
- Full-building animation sheet -> avoided.

## Packing Machine Design Rule

The herb packing/bundling machine should be modular:

- Static machine body.
- Separate press plate or packing jaw.
- Separate crank/gear/wheel.
- Separate twine spool or small wheel.
- Optional small belt/feed strip sheet.
- Input tray overlay states.
- Bundle output sprite states.
- Status lamp/glow overlay.
- Optional herb fleck/dust particles.

The machine should not be one giant animated sheet.

## Current Footprint Constraints

Keep the measured drying-room footprint from the current plan:

- Process module area: `x=535 y=367 w=456 h=230`.
- Bundler drop zone: `x=550 y=406 w=254 h=190`.
- Machine nominal area: `x=555 y=411 w=254 h=164`.
- Machine center: `x=682 y=493`.
- Machine visible safe extents: approx `x=564..857 y=404..604`.
- Maximum machine-body art footprint: `330 x 210`.

Any new packing-machine art should fit that footprint unless the room layout is deliberately redesigned.

## Recommended Minimal Frame Plan

Use:

- Machine body: 1 static sprite.
- Press plate / jaw: 1 sprite, moved with Phaser tween.
- Gear/crank: 1 sprite, rotated with Phaser tween.
- Twine spool/wheel: 1 sprite, rotated with Phaser tween.
- Belt/feed strip: optional 4-6 frame loop.
- Status glow/lamp: alpha pulse or 2-4 frame loop.
- Bundle output: 3 sprite states, `empty / forming / finished`.
- Particles: generated at runtime, no full sprite sheet required.

## Suggested Machine States

- `Idle`: stopped, dim/off glow.
- `Loaded`: ingredients visible, gentle lamp pulse.
- `Packing`: press cycles, gear/spool rotates, optional belt loops, small particles.
- `Ready`: finished bundle visible with ready glow.
- `Blocked`: warning pulse, no press motion.

## Plan Update Performed

Updated:

`C:\Users\yrred\Desktop\Unity\TWB-Farming\Herbalist_Drying_Room_Asset_Measurements_And_Creation_Plan.md`

Added a new section:

`Packing / Bundler Machine Layered Animation Rule`

The plan now states that the packing machine should be built as layered Phaser sprites/tweens/particles, not as a full-machine sprite sheet.

## Risks

- If this principle is promoted too broadly without the Phaser translation, future workers may copy Unity-prefab wording too literally.
- The current candidate package includes a broad `bundler_machine_body`; a future revision may need to split that into smaller packing-machine parts before runtime install.
- The animation should stay readable at the current room scale. Too many moving details may become visual noise.

## Memory-Worthy Notes

- Use layered machine animation for Garden machinery: static body, small moving child sprites, transform tweens, glow overlays, particles, and limited sprite swaps.
- Avoid giant full-machine sprite sheets for multi-state machines.
- For the herb packing machine, keep the measured `330 x 210` machine-body footprint unless the room layout is intentionally redesigned.

## Do Not Promote Yet

- Do not promote the exact mine prefab structure as a Garden requirement.
- Do not promote Unity-specific implementation names for the Phaser project.
- Do not promote the current packing-machine visual candidate as final art; it may need a layered revision.

## Mini Handoff For Orchestrator

User provided important research on efficient layered animation for automated machines. I translated the principle from a WW1 magitech mine example into Glassroot Garden's Phaser packing/bundling machine plan. The key decision candidate is: build the packing machine as a layered object with a static body, small rotating/sliding parts, particles, glow overlays, and sprite swaps, not as one full animated machine sheet. The measured machine safe footprint remains `330 x 210`, centered around `x=682 y=493` in the drying-room process module. Please review for promotion as a Garden machinery animation guideline before the next asset/runtime install pass.
