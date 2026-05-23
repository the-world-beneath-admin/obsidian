# Design Constraints

## Summary

Scope: World Key: Glassroot Garden.

Glassroot Garden should stay small, readable, and evidence-driven. The MVP should prove that the visible garden loop and Companion automation feel good before adding broad economy or narrative systems.

## Memory Items

- Decision - Do not build giant alchemy recipes, player-to-player marketplace, direct main-game item rewards, generated story dig sites, plant breeding genetics, full NPC economy, weather simulation, open-world exploration, real poison/herbal instruction content, Companion breeding/trading, farm building placement, social visiting, or leaderboards in MVP.
- Decision - No crop death in MVP.
- Decision - Failure should feel funny or interesting rather than cruel.
- Decision - Use existing companion icons as roaming holo-companion tokens first, then upgrade to mini-sprites later.
- Decision - Use existing `platform_game_saves` JSON for MVP garden state only through dedicated server-owned routes; move to normalized D1 tables before wider public economy.
- Warning - The generic platform inventory event endpoint should not be used directly by the browser client to mint harvest rewards.
- Source: [[memory/raw/game-design/glassroot/TWB_Glassroot_Garden_GPT_Pro_Research_Plan]]
