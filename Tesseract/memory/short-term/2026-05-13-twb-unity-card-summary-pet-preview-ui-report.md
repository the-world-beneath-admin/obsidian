# TWB Unity Worker Report - 2026-05-13 - Card Summary Pet Preview UI

## Task

Tighten the dungeon pet-preview Card Summary window: move the header down, restyle the action buttons to the minimalist local style, remove Salvage from the dungeon-selection preview variant, and make Back return to the dungeon pet picker instead of causing broader window switching.

## Result

Implemented in `CardSummarySurfaceBuilder.cs`. The Card Summary header is 15 pixels lower, Back/Salvage/Confirm now use a minimalist button treatment, Salvage is visible only for the real Archive return target, and dungeon-party Back now restores the archive picker overlay without closing the underlying dungeon flow.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\CardSummarySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-card-summary-pet-preview-ui-report.md`

## Checks run

- `git diff --check -- Assets/_TWB/Scripts/UnityBridge/UI/Builders/CardSummarySurfaceBuilder.cs` passed, with only the existing LF-to-CRLF warning.
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 warnings and 0 errors.
- Unity batch compile was attempted, but the project was already open in another Unity instance, so batchmode could not run.
- The exact Unity compiler command from the editor response files was run manually and passed with exit code 0.

## Cleanup performed

Removed the failed throwaway Unity automation run folder created by the blocked batchmode attempt.

## Risks

The open Unity editor status still reports the last stale compile failure from before the helper methods were visible to Unity. Current source and the Unity compiler response-file invocation both compile cleanly; the editor needs a fresh import/domain reload after leaving the currently open session or clearing the stale console state.

## Memory-worthy notes

The dungeon-selection Card Summary should behave as a modal preview layered over the dungeon archive picker: Back returns to the picker, Confirm commits and collapses the picker flow, and Salvage belongs only to the real Archive card detail view.

## Do not promote to memory

Exact pixel offsets and temporary styling values are implementation details unless they become a durable UI standard.

## Next recommended gate

After the open Unity editor refreshes scripts, verify the pet preview visually from the dungeon slot picker: header below the frame lip, minimalist Back/Confirm buttons, no Salvage button in this flow, and Back returning directly to the pet picker.
