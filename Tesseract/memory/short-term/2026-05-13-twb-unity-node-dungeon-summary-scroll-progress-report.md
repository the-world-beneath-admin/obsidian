# TWB Unity Worker Report - 2026-05-13 - Node Dungeon Summary Scroll Progress

## Task

Main game / The World Beneath. Redo the world-map Node Dungeons summary panel so dungeon selection rows are scrollable, only three are visible at once, the information display has more room, and a Node Progress bar fills from 0-100% between the information area and the dungeon selector rows.

## Result

Implemented the UI layout pass in `WorldMapSurfaceBuilder.cs`.

The Node Dungeons panel now has:

- A taller node information panel.
- A dedicated `NODE PROGRESS` bar using the representative node's `NodeProgressPercent` and `NodeProgressStateText`.
- A masked `ScrollRect` for dungeon selection rows.
- Three visible dungeon rows at a time, with additional rows available by scrolling.
- A compact scroll hint when more than three traces are available.

The underlying dungeon selection behavior is unchanged: clicking a row still selects the same world dungeon and opens the inspect window.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-unity-node-dungeon-summary-scroll-progress-report.md`

## Checks run

From `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`:

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed.
  - Existing warnings only:
    - `UIShellBootstrap.cs(370,22): warning CS0649: _craftCreateV2SummaryName is never assigned`
    - `WorldMapSurfaceBuilder.cs(645,24): warning CS0649: FoldedContributorGlyphs is never assigned`
- `git diff --check` on `WorldMapSurfaceBuilder.cs`
  - Passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Reported `Status: probably-clean`, `UnityExitCode: 0`, `ErrorSignals: 0`, `WarningSignals: 0`.
  - Batchmode also reported that another Unity instance already has the project open, so this was not a full independent Unity compile session.

## Cleanup performed

No scratch files or screenshots were created. Unity automation logs were retained under `artifacts\unity-automation\` as check evidence.

## Risks

This was code/build verified, not visually verified in the live Unity editor from this worker. The user should reopen or refresh the Node Dungeons panel in the editor to judge final spacing and scroll feel.

The project worktree is heavily dirty and `WorldMapSurfaceBuilder.cs` appears untracked from git's current perspective; this report does not attempt cleanup, staging, or source-control correction.

## Memory-worthy notes

Node Dungeons summary now uses a three-visible-row scroll model and an explicit Node Progress bar rather than burying progress in list metadata.

## Do not promote to memory

Do not promote as final visual acceptance until the user verifies the live Unity panel.

## Next recommended gate

Refresh the world-map Node Dungeons panel in Unity and tune pixel spacing if the scroll viewport or progress bar needs adjustment after visual inspection.
