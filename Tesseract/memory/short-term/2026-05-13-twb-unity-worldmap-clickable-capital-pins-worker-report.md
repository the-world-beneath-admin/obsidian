# TWB Unity Worker Report - 2026-05-13 - Clickable World Capital Pins

## Task

Make 2400km WORLD map capital pins clickable and show a compact town/capital description popup when selected.

## Result

Capital pins are now interactive `Button` targets. Clicking a capital stores the selected capital label id, refreshes the activities world map, preserves the selected marker through collision filtering, and displays a compact map-anchored info popup. The popup includes the town/capital name, a short WORLD-map description, coordinates, current zoom, and a Close button.

The popup is clamped inside the map area and uses the existing HoloGlyph panel/text/button helpers. Local/region town pins, route/lane systems, dungeon summary UI, generated capital catalog contents, and Node Progress logic were not changed.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 2 existing CS0649 warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - passed / `probably-clean`, 0 error signals, 0 warning signals.

## Cleanup performed

No temporary files were created.

## Risks

Visual placement and copy should be reviewed in the live Unity editor. The popup is intentionally generic because the current generated capital catalog only contains id, display name, coordinates, min zoom, and priority; it does not include rich town/country descriptions.

## Memory-worthy notes

WORLD capital pins now have a first interaction layer. Richer descriptions would require adding or generating a proper capital metadata source rather than embedding ad hoc prose into the UI builder.

## Do not promote to memory

Do not promote the temporary popup copy as final lore/content.

## Next recommended gate

Click several WORLD 2400km capital pins in the editor and tune popup placement/copy if the window clashes with dense marker clusters.
