# Controls

## Summary

Scope: World Key: Glassroot Garden.

The prototype uses mouse/tap-friendly browser controls with drag/drop and click fallbacks. The design should avoid hover-only or tiny hitbox interactions so it can remain testable and mobile-adaptable.

## Memory Items

- Fact - Seed Bag opens and seeds can be dragged onto plots.
- Fact - A click-to-select seed fallback was added because browser automation did not reliably trigger Phaser drag events on seed packets.
- Fact - Raw herbs can be dragged to the drying rack, with a click fallback from raw herb to drying rack.
- Fact - Dried herbs can be dragged into the Bundler, and incorrect herb/order is rejected.
- Decision - Keep click fallbacks where drag/drop is important, because they improve accessibility and make regression testing more reliable.
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]
