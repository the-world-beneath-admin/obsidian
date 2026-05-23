# TWB Unity Worker Report - 2026-05-13 - Dungeon Party Modal Archive Picker

## Task

Main game / The World Beneath. Change the world-map dungeon Commit Pets flow so changing a slot opens an additional archive picker window instead of replacing the inspect dungeon window, then collapses the picker stack back to the inspect window after pet commit.

## Result

Added a world-map-local dungeon archive picker window. The dungeon inspect window now stays open while selecting a replacement pet. Archive card selection still reuses the existing card summary / confirm path, but the archive return path now detects the world-map picker and closes that stacked picker flow instead of switching apps. After confirm, the picker closes and the activities/world-map surface refreshes back to the inspect window with the updated party slot.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\CardSummarySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-dungeon-party-modal-archive-picker-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with two existing CS0649 warnings.
- `git diff --check -- "Assets/_TWB/Scripts/UnityBridge/UI/Builders/WorldMapSurfaceBuilder.cs" "Assets/_TWB/Scripts/UnityBridge/UI/Builders/CardSummarySurfaceBuilder.cs" "Assets/_TWB/Scripts/UnityBridge/UI/UIShellBootstrap.cs"` - reported pre-existing trailing whitespace in unrelated `UIShellBootstrap.cs` diff lines.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` - returned `probably-clean`, `UnityExitCode: 0`; automation noted another Unity editor instance already had the project open.

## Cleanup performed

No temporary files were created by this pass.

## Risks

Needs visual/manual verification in the open Unity editor for stacked ordering: inspect window, archive picker, then card summary confirm. The compile path is clean, but batchmode could not open a second editor instance.

## Memory-worthy notes

World-map dungeon slot changes now use a stacked modal picker flow instead of navigating the whole manifest to Archive.

## Do not promote to memory

Do not promote the local implementation details unless this stacked picker pattern becomes the standard for Archive-based selection elsewhere.

## Next recommended gate

Manual smoke: Inspect Dungeon -> Change slot -> pick archive card -> Confirm -> verify archive and card summary close, inspect remains, and the chosen card appears in the correct slot.
