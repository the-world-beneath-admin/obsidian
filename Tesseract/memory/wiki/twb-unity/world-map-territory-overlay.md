# TWB Unity World Map Territory Overlay

## Summary

The main Unity world map territory overlay is moving away from heatmap-style dungeon/territory presentation toward clustered display-owner nodes, influence fields/rims, routes/lanes, and node-level dungeon interaction.

## Durable Rules

- World map region/area modes should show owner summaries rather than every folded dungeon or anchor as a standalone object.
- Visible town labels should act as display owners.
- Standalone owner node/markers should be suppressed when they duplicate a visible label.
- Folded child anchors should become owner badges/intensity instead of independent map clutter.
- Territory connections should attach to display owners, not raw/folded child anchors.
- Node dungeon interaction should open a movable subwindow summarizing available dungeons at the clicked node.
- WORLD capital markers should use a dedicated display asset at overview scale rather than the detailed full pin.
- WORLD capital markers should be clickable Button targets that open a compact map-anchored popup and preserve the selected capital label id through map refreshes.
- World-map dungeon reward testing may use a temporary editor/debug-only `DEV COMPLETE` path, but it must remain test-facing and must not alter normal dungeon run timing or final gameplay balance.
- The dungeon reward claim path should continue through the normal claim command and reward application flow.

## Current Risks

- Route/lane presentation is still not final.
- Line readability and long-range route connectivity need focused diagnosis.
- Collapsed town marker/text behavior still needs a final rule.
- WORLD capital marker readability and popup placement at 2400km zoom still need live visual confirmation, and richer descriptions need a proper capital metadata source.
- Node dungeon and inspect dungeon windows are functional but not visually finished.
- The `DEV COMPLETE` path is build-verified only; it needs live editor click-through before being trusted as a test helper.
- The cleaned claim rewards modal needs live visual verification before it is treated as visually final.
- Unity batchmode/status reports can be misleading while the project is open in another editor instance; inspect log context before treating shutdown or editor-lock noise as a product failure.

## Read-First Implementation Files

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\WorldMapService.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\UIBoundary\WorldMapUiSnapshot.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\WorldMap\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\WorldMapDungeons\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\WorldMapDungeons\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\UIBoundary\Commands\ClaimWorldMapDungeonRunCommand.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\UIBoundary\UiWorldMapCommandHandler.cs`

## Sources

- [[short-term/2026-05-12-twb-unity-worldmap-working-window-intake]]
- [[short-term/2026-05-15-twb-unity-run-rewards-dev-complete-report]]
- [[short-term/2026-05-16-twb-main-game-worker-final-decommission-report]]
