# TWB Unity Worker Report - 2026-05-13 - Worldmap Capital Pin Display LOD

## Task

Analyze why the 2400km WORLD map capital pins looked pixelated/noisy after being enlarged, then implement a non-blind fix.

## Result

The issue was a combination of asset-detail mismatch and runtime loading behavior. The 1024px ImageGen pin was too detailed for a 30-40px UI marker, and the marker loader preferred loading PNGs directly from disk, bypassing Unity sprite importer settings such as mipmaps.

Implemented a dedicated display LOD sprite for WORLD capital markers and wired that path into the capital marker renderer. The LOD uses the same cyan/gold HoloGlyph language but removes micro-detail so it reads cleanly at small map scale. The WORLD capital marker path now prefers an imported Sprite and uses mipmapped/trilinear sampling when requested, with a mipped disk fallback if the asset has not imported yet.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_display_lod_256.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_display_lod_256.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\README.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 2 existing CS0649 warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - failed due Unity editor log service/connectivity errors, not C# compile errors. The relevant log included Unity Connect/Project ID 401 and curl timeout messages.

## Cleanup performed

Temporary visual contact-sheet previews were removed from the user temp folder.

## Risks

The new LOD needs a live visual pass in the editor to confirm it reads well against the 2400km map background. Larger marker footprints may fold a few edge/dense capitals, which is expected but should be reviewed visually.

## Memory-worthy notes

The 2400km WORLD map capital pins should use a display-scale LOD sprite, not the detailed high-resolution source pin directly. The capital marker path also needs imported/mipped sprite loading to avoid noisy downsampling.

## Do not promote to memory

Do not promote exact LOD size values or the temporary preview comparison details until visual review approves them.

## Next recommended gate

Refresh the Unity editor, open the 2400km WORLD map, and confirm the capital pins are clear without crowding the overview.
