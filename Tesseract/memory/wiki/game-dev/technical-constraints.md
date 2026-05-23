# Technical Constraints

## Summary

Scope: World Key: Glassroot Garden and shared TWB platform integration.

The local prototype is a Phaser 3.90, TypeScript, Vite browser game. The longer-term production direction is same-origin deployment under the existing TWB website with Cloudflare Worker and D1 as the server authority.

## Memory Items

- Fact - Local source candidate: `C:\Users\yrred\Desktop\Unity\TWB-Farming`.
- Fact - Package name is `twb-glassroot-garden`.
- Fact - Build stack is Phaser `^3.90.0`, TypeScript `^5.9.0`, and Vite `^7.0.0`.
- Fact - Available package scripts are `npm run dev`, `npm run build`, and `npm run preview`.
- Fact - Confirmed build/test commands are recorded in [[build-test-commands]].
- Decision - Browser game should eventually live under `https://the-world-beneath.com/world-keys/glassroot/`.
- Decision - API namespace should be `/api/world-keys/glassroot/*`.
- Warning - Client-side game state is acceptable for local prototype work, but reward-bearing public play needs Worker-owned planting, growth, harvest validation, Companion locks, and ledger writes.
- Source: `memory/raw/game-design/glassroot/package.json`
- Source: [[memory/raw/game-design/glassroot/TWB_Glassroot_Garden_GPT_Pro_Research_Plan]]
- Source: [[build-test-commands]]
