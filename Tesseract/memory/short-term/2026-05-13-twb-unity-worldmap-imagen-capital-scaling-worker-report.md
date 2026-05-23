# TWB Unity Worker Report - 2026-05-13 - Worldmap ImageGen Capital Scaling

## Task

Replace the hand-built world capital display LOD with an ImageGen-derived asset and correct the actual scaling/runtime rendering issue for 2400km WORLD map capital pins.

## Result

The rejected hand-built display LOD was removed. A new ImageGen-derived capital pin was copied into the Unity project as a source asset and a trimmed display asset. The WORLD capital marker path now points at the ImageGen display asset.

The scaling fix remains in code: the capital marker loader now prefers the imported Sprite, uses mipmapped/trilinear sampling for this path, has a mipped disk fallback, and snaps marker anchors to whole parent pixels to reduce tiny-marker sampling artifacts. Marker sizes were nudged slightly upward so the visible pin reads at world scale without relying on a bad hand-painted simplification.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_imagen_display_512.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_imagen_display_512.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_imagen_source_1024.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_imagen_source_1024.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\README.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 2 existing CS0649 warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - passed / `probably-clean`, 0 error signals, 0 warning signals.

## Cleanup performed

Removed the rejected hand-built `twb_map_pin_world_capital_display_lod_256.png` and its `.meta`. The original ImageGen output under `.codex\generated_images` was left intact.

## Risks

The new ImageGen display asset still needs live visual review at 2400km WORLD zoom. If it remains noisy, the next correction should stay in the scaling/import/sprite path or use a new ImageGen prompt with fewer internal rings, not manual painting.

## Memory-worthy notes

The capital pin issue was a runtime scaling/import path problem as much as an art problem. The world capital marker path should use imported/mipped Sprite loading and pixel-snapped anchors.

## Do not promote to memory

Do not promote the rejected hand-built display LOD.

## Next recommended gate

Refresh the editor and inspect the 2400km WORLD map capitals with the ImageGen display asset active.
