# TWB Unity Worker Report - 2026-05-12 - Dungeon Inspect Header Command Fix

## Task

Main game / The World Beneath. Fix the follow-up visual issues in the world-map dungeon inspect modal: the header bar was hanging over the frame, and the Start Run button was overhanging the lower frame element.

## Result

Moved the inspect header down and inward so it sits inside the modal shell safe area. Lowered the three content columns to maintain spacing below the header.

Moved the Start Run / Recall Team command from the modal root into the Commit Pets panel, then shortened the pet-slot stack to reserve an internal command strip. This keeps the command inside its own panel instead of floating over the outer frame.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-unity-dungeon-inspect-header-command-fix-worker-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed with 0 errors. Two pre-existing CS0649 warnings remain.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - probably-clean, 0 error signals, 0 warning signals.

## Cleanup performed

No temporary files were created in this follow-up pass.

## Risks

The exact visual result still needs one more editor look at 1920x1080 because this was adjusted from the screenshot and source anchors rather than a captured Unity Game-view screenshot.

## Memory-worthy notes

For the dungeon inspect modal, root-level controls should avoid the decorative frame safe area. Header bars and command buttons should sit inside inset content/panel bounds.

## Do not promote to memory

Do not promote the precise anchor values as final standards unless the editor visual pass confirms them.

## Next recommended gate

Reopen the dungeon inspect modal in the Game view and confirm the header sits under the top shell lip and Start Run stays contained inside Commit Pets.
