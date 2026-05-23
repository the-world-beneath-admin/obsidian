# The Garden Decisions

## Active Decisions

- Decision - Use The Garden as the public title; Glassroot Garden remains the internal/source name unless renamed later.
- Decision - Use "Companion" in UI terminology where practical.
- Decision - Seed planting should be mobile-friendly: select a seed, then use Plant Selected. Do not rely on drag/drop planting.
- Decision - Storage/workbench presentation should feel like an old herbalist or alchemical workbench, not a full room or a data dashboard.
- Decision - Raw, drying, dried, compost, finished bundle, and Notice Board information should live near the relevant object rather than in one general summary strip.
- Decision - Notice Board contracts give XP, rewards, and Notice Board completion credit.
- Decision - Notice Board quest bundles are currently one-off orders: open -> awaiting completion -> complete. Duplicate production is blocked once queued or completed.
- Decision - Transfer Bundles move outputs to World Key shared storage and do not give XP.
- Decision - Transfer Bundles remain repeatable even while Notice Board quest bundles are one-off.
- Decision - Notice Board and Transfer Bundle recipe definitions should live in `src/data/bundleCatalog.ts` rather than being buried in the main scene.
- Decision - Generated Notice Board orders should use 3 distinct plant inputs with varied quantities.
- Decision - Raw/dried bins are scrollable plant storage surfaces with high local caps, currently 999 units each, not whole-bin compost controls.
- Decision - The Herbalist Workbench room direction is image-backed: basement brick/floor backdrop, wooden work table, wall-mounted drying rack, ornate Notice Board, and image-backed storage panels.
- Decision - Require landscape mode for the Herbalist Workbench / Storage Hut mobile review; portrait `1280 x 720` Scale.FIT is too small.
- Decision - Tier unlock requirements are 200 T1 XP/units for T2, 500 T2 for T3, 1000 T3 for T4, and 10000 T4 for T5.
- Decision - XP should appear as floating ticks at action locations rather than many static XP indicators.
- Decision - Comfreygrass is a free compost filler plant. It does not consume ready compost and harvests into curing compost.
- Decision - Normal plant growth timing is tier-based: T1 60s, T2 90s, T3 120s, T4 180s, T5 240s. Comfreygrass remains 120s.

## Compatibility Notes

- The internal id for Comfreygrass remains `middenbloom` for compatibility. Do not rename the id directly without a save migration plan.

## Sources

- [[short-term/2026-05-12-glassroot-garden-working-window-intake]]
- [[short-term/2026-05-17-garden-worker-final-decommission-report]]
- [[short-term/2026-05-17-glassroot-garden-notice-board-lifecycle-hardening-report]]
- [[short-term/2026-05-18-glassroot-garden-worker-report]]
- [[short-term/2026-05-19-glassroot-garden-worker-final-decommission-report]]
- [[wiki/game-dev/world-keys]]
