# HoloGlyph UI Style

## Summary

The main Unity UI is moving toward a HoloGlyph / field-tablet visual language: dense functional panels, large sci-fi frames, cyan glow, orange accents, and readable tool-like interaction surfaces.

## Durable Style Rules

- Use cyan outlines, title areas, dropdown areas, and info areas.
- Use orange slot outlines.
- Use reduced or faded cyan fills for slot backgrounds.
- Prefer functional dense tool panels over landing-page style composition.
- The style is for crafting, activities, home defense, world-map navigation, dungeon inspection, and related Unity UI surfaces.
- Generated HoloGlyph material, catalyst, modifier, skill, and currency icon sets are installed as Unity sprites under `Assets/Resources/GameArt/TWB_HoloGlyph_T1/Icons`.
- Inventory V2, Craft Create V2, and Craft Apply V2 should use the current HoloGlyph item icon resolver path.
- Modifier inventory ids use `card_mod_*`, while generated modifier icon files use `mod_*`; icon resolution must bridge that naming mismatch.

## Do Not Promote

- Temporary debug colors.
- One-off layer toggles.
- Visual attribution names.
- Diagnostic counters.
- Screenshots as final specs unless Bob/orchestrator curates them explicitly.
- The temporary world-map `DEV COMPLETE` button as final player-facing UI.
- Build-only claims that every future UI surface is icon-wired.

## Sources

- [[short-term/2026-05-12-twb-unity-worldmap-working-window-intake]]
- [[short-term/2026-05-15-twb-unity-icon-wiring-audit-report]]
- [[short-term/2026-05-16-twb-main-game-worker-final-decommission-report]]
