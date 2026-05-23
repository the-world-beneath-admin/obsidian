# TWB Unity Worker Report - 2026-05-15 - Card Summary Confirm Button

## Task

Fix the companion/card summary confirm button so it works from the dungeon pet assignment preview and sits in the lower-right position indicated by the user.

## Result

Implemented a narrow UI/action-path fix. The Card Summary confirm button is now explicitly anchored in the lower-right action strip during build and refresh, and its child decorative/text graphics no longer act as raycast targets over the button root.

Fixed the inert confirm path for already-filled dungeon slots by preserving `_archivePendingDungeonSlot` before opening Card Summary from both the world-map dungeon summary and the older activities dungeon slot surface.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\CardSummarySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\DungeonSurfaceBuilder.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 errors and 2 existing warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` was attempted but batchmode could not open because the project is already open in Unity.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` reports one existing editor-log error signal from Unity Services auth/project-id 401, not from this compile change.

## Cleanup performed

No source cleanup or generated asset cleanup was needed. Unity automation left its normal diagnostic artifact folder for the blocked compile attempt.

## Risks

Live click verification still needs a quick in-editor reload/click pass because batchmode compile was blocked by the open Unity editor.

## Memory-worthy notes

The silent confirm failure was caused by opening Card Summary for an already-assigned dungeon slot without setting the pending dungeon slot. Confirm then returned early because `_archivePendingDungeonSlot` was 0.

## Do not promote to memory

Do not promote the transient Unity Services 401 status failure unless it repeats as a real workflow blocker.

## Next recommended gate

After Unity reloads scripts, manually open the dungeon pet assignment flow, click an assigned/shared companion card, confirm from the lower-right button, and verify it returns to the dungeon summary with the slot preserved.
