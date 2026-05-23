# TWB Unity Worker Report - 2026-05-13 - Worldmap Imagegen Capital Pin

## Task

Wire in the improved ImageGen-created minimalist capital pin for the 2400km WORLD map capital markers in the main game / The World Beneath Unity project.

## Result

World map capital markers now load the high-resolution transparent ImageGen asset through the Unity Resources path. The rejected 256px scratch pin was removed so the world-map capital layer no longer has a bad fallback asset hanging around.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_minimal_1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_minimal_1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\README.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 2 existing CS0649 warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - passed / `probably-clean`, 0 error signals, 0 warning signals.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` - could not open batchmode because the Unity editor already had the project open; automation still reported `probably-clean`.
- Follow-up `status` check - `probably-clean`, 0 error signals, 0 warning signals.

## Cleanup performed

Removed the rejected `twb_map_pin_world_capital_minimal_256.png` scratch asset and its `.meta`.

## Risks

Unity batch compile/import did not fully run because the editor instance already had the project open. The next editor refresh should import the new `.meta` normally, and C# build/status are clean.

## Memory-worthy notes

The 2400km WORLD map should use a dedicated high-resolution minimalist capital pin asset instead of reusing the local/region town pin art at tiny scale.

## Do not promote to memory

Do not promote the rejected 256px scratch pin attempt or any temporary visual tuning details.

## Next recommended gate

Refresh the Unity editor and visually confirm the 2400km WORLD map capital markers use the new high-res pin cleanly at runtime scale.
