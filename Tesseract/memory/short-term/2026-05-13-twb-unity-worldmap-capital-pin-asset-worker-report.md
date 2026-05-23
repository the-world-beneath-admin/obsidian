# TWB Unity Worker Report - 2026-05-13 - Worldmap Capital Pin Asset

## Task

Replace the poor WORLD zoom capital marker presentation with a custom minimalist asset that still fits the existing TWB map pin family.

## Result

Created a dedicated transparent 256px world-scale capital pin asset with smoked-glass fill, cyan tactical contour, and gold signal nodes. The 2400km WORLD capital-marker renderer now uses this custom asset directly. Region/local map pins continue using the existing detailed supplied town pins.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_minimal_256.png`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\Resources\GameArt\TWB_HoloGlyph_T1\WorldMap\Markers\Towns\twb_map_pin_world_capital_minimal_256.png.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\README.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` reported `Status: probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.

## Cleanup performed

Deleted throwaway 14px/16px/18px preview images created under `diagnostics\worldmap`.

## Risks

The asset is hand-generated in-project rather than produced by the full image pipeline. It is visually aligned to the existing pin family, but may still need one editor screenshot tuning pass for exact size and density.

## Memory-worthy notes

Full detailed map pins work well at region/local zoom but are too ornate for 2400km WORLD scale. WORLD capitals need a dedicated minimal asset, not a downscaled full pin.

## Do not promote to memory

Do not promote temporary preview paths or build warning repetition.

## Next recommended gate

Reload the WORLD 2400km view and visually inspect whether the new minimalist capital pin reads cleanly against the generated world tiles.
