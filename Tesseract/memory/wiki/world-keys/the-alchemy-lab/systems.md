# The Alchemy Lab Systems

## Core Loop

The current prototype loop includes:

1. Import herb bundles from shared inventory.
2. Break down herb bundles into lab materials.
3. Store materials in lab storage.
4. Craft at the alchemy table.
5. Place finished products on the finished rack.
6. Generate regular outputs and essence bundle outputs.
7. Send pets into the cave to retrieve cave materials.
8. Export selected outputs back into shared World Key inventory.

## Cave Exploration

- Cave exploration should be an explorable top-down maze, not a node-and-line system.
- Cave art direction is top-down orthographic / 2.5D tiled-map pixel-art RPG style.
- Player-placed torches/lights have been removed from the cave loop.
- Recent work widened cave paths, separated wall-frame tiles from pet-travel tiles, added direct walkable return paths to the shed, smoothed cave redraws, and increased pet movement speed.

## Pet Behavior

- Pets automate cave gathering rather than farming.
- Pets release from the shed one at a time.
- Current release interval: 30 seconds.
- Sleep cooldown starts after the pet reaches the shed and unloads, not when energy hits zero.

## Inventory

- Current shared inventory is prototype browser localStorage.
- Essence outputs are intended to become shared inventory bundles for another World Key to use.

## Sources

- [[short-term/2026-05-12-twb-alchemy-working-window-intake]]
- [[wiki/world-keys/shared-inventory]]
- [[wiki/world-keys/pets]]
