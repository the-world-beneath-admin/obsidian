# World Key Shared Inventory

## Summary

The current World Key prototypes use local browser storage to model shared inventory, but this is prototype scaffolding, not the final account-backed contract.

## Current Facts

- The Garden and The Alchemy Lab are intended to share umbrella inventory concepts.
- The Alchemy Lab currently imports herb bundles, breaks them down, crafts outputs, and can produce essence bundle outputs intended for another World Key.
- TWB Alchemy currently uses browser `localStorage` for shared inventory and alchemy state.
- The website Cloudflare Worker already has account-backed platform inventory tables and APIs, but Garden/Alchemy still need attachment work.
- The final shared inventory schema across World Keys is still open.

## Rules

- Do not promote current `localStorage` keys as final production API contracts.
- Do not treat browser-local storage as secure or authoritative.
- Future production integration should define account-backed persistence, schema migration, and server-side reward/inventory authority.
- Materials remain game-local unless a game explicitly exports them to shared platform inventory through a named platform event.

## Open Questions

- What is the final shared inventory schema across The Garden, The Alchemy Lab, and future World Keys?
- What website route or launcher contract should register World Key inventories?
- What backend service replaces localStorage for shared inventory and saved game state?
- Which Garden outputs become shared platform items?
- Which Alchemy outputs become shared platform items?

## Sources

- [[short-term/2026-05-12-twb-alchemy-working-window-intake]]
- [[wiki/game-dev/world-keys]]
- [[wiki/shared-platform/inventory-boundaries]]
