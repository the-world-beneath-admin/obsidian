# TWB Unity Worker Report - 2026-05-13 - Worldmap Capital Markers

## Task

Add country-capital city markers to the main-game world map at the 2400km WORLD zoom view, using the supplied TWB map pin assets rather than generated placeholder marker art.

## Result

Implemented a generated Natural Earth capital-marker catalog and wired the WORLD zoom place-label path to render capital pins only for the 2400km world view. The renderer uses the existing supplied town pin sprites under Unity `Resources` and avoids baking markers into the map tiles.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\WorldMap\WorldMapCapitalMarkerGeneratedCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\WorldMap\WorldMapPlaceLabelDataCatalog.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.Domain.csproj`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\overlay\generate-world-capital-markers.py`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\tools\worldmap\overlay\generate-world-capital-markers.ps1`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\diagnostics\worldmap\world_capital_markers_report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` could not run batchmode because the Unity editor already had the project open; automation reported `Status: probably-clean` and `UnityExitCode: 0`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` reported `Status: probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.

## Cleanup performed

No scratch files were created outside the generated capital catalog/report and Unity automation evidence.

## Risks

The capital catalog uses Natural Earth `ADM0CAP=1`, which includes 200 capital markers because a few countries or admin-0 entities have multiple capital entries. The visual pass still needs an editor look to tune pin size/density in high-density areas such as Europe.

## Memory-worthy notes

The 2400km WORLD zoom now has a separate capital-marker path keyed by `world_capital_` labels. Region/detail zooms continue using the existing overview/town label behavior.

## Do not promote to memory

Do not promote raw generated TSV contents or transient Unity automation log paths.

## Next recommended gate

Open the WORLD 2400km map view in the Unity editor and visually tune marker size/density if the new supplied pins read too large or crowded.
