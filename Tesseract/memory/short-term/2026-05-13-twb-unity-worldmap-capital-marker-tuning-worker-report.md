# TWB Unity Worker Report - 2026-05-13 - Worldmap Capital Marker Tuning

## Task

Fix the 2400km WORLD zoom capital markers after the full detailed town pins looked muddy at world scale.

## Result

Adjusted only the WORLD capital-marker renderer. It now uses a compact locator-medallion crop from the supplied city pin asset and smaller 14-18px sizes. Region/local marker presentation remains on the normal supplied full-pin path.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` reported `Status: probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.

## Cleanup performed

No temporary files were created.

## Risks

Needs a visual editor check to confirm the cropped supplied-pin marker reads cleanly across dense regions.

## Memory-worthy notes

Full TWB town pins look good at region/local scale but are too detailed for 2400km WORLD zoom. WORLD capital markers should use a compact marker treatment derived from the supplied pin art.

## Do not promote to memory

Do not promote transient warning counts or build timing.

## Next recommended gate

Review the WORLD 2400km view and decide whether to keep the compact medallion or make a dedicated artist-authored world-scale capital pin asset.
