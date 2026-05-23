# TWB Unity Worker Report - 2026-05-13 - Worldmap Capital Pin Size

## Task

Increase the 2400km WORLD map capital pin visibility after the new minimalist ImageGen asset proved too small in the live map view.

## Result

WORLD capital marker sizing was raised from a 14-18px range to a 30-40px range, with the non-world fallback raised from 34px to 42px. This keeps the change local to capital markers and does not alter local/region town pin sizing.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 2 existing CS0649 warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - passed / `probably-clean`, 0 error signals, 0 warning signals.

## Cleanup performed

No temporary files were created.

## Risks

Larger capital pins may need one more visual tuning pass if dense areas begin to feel crowded at 2400km zoom.

## Memory-worthy notes

The high-resolution WORLD capital marker asset needs a much larger runtime size than the previous scratch pin to stay legible on the 2400km overview.

## Do not promote to memory

Do not promote the exact temporary size values unless they survive visual review.

## Next recommended gate

Refresh the 2400km WORLD map and confirm capital pins are readable without overwhelming the overview.
