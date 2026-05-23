# The Alchemy Lab

## Summary

The Alchemy Lab is the public World Key title for the standalone browser alchemy mini-game. The current source project is `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.

## Scope

- Parent project: The World Beneath.
- World Key: The Alchemy Lab.
- Source/project name: TWB Alchemy.
- Code directory: `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.
- Stack: Vite, Phaser 3.90, TypeScript.
- Current scope: local browser mini-game prototype.
- Not in scope: main Unity game implementation, account-backed persistence, production website routing, final art tileset, or production shared-inventory backend.

## Current Prototype State

Implemented:

- brick-walled city basement alchemy lab UI
- shared inventory prototype via local browser storage
- herb bundle import and breakdown
- lab storage
- alchemy table crafting
- finished product rack
- crafting XP and unlocks
- regular outputs and essence bundle outputs
- trapdoor to cave view
- tiled cave maze art pass
- autonomous pet cave exploration
- energy drain, return-home behavior, sleep cooldown
- resource harvesting
- node despawn/respawn
- staggered pet release from the shed

The task has shifted toward release planning and scope clarification: the current target is a two-screen World Key with a harvesting cave and a one-screen three-stage crafting machine, but the exact design still needs Bob/orchestrator review.

## Build And Test

Run from `C:\Users\yrred\Desktop\Unity\TWB-Alchemy`.

- Dev server: `npm run dev`
- Build: `npm run build`
- Preview: `npm run preview`
- Current smoke URL: `http://127.0.0.1:5174/`

## Sources

- [[short-term/2026-05-12-twb-alchemy-working-window-intake]]
- `C:\Users\yrred\Desktop\Unity\TWB-Alchemy\package.json`
