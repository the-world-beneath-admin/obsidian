# TWB Unity Worker Report - 2026-05-15 - Shared Companion Conflict Model Slice

## Task

Implement slice 7 of the Unity persistence/account integration plan for The World Beneath: a non-mutating shared companion assignment conflict model for local activity prep.

## Result

Completed. Unity now has one read-only assignment conflict model for Archive/Card Summary assignment prep. It normalizes local dungeon locks, local Home Defense assignments, cached shared companion account locks, missing account projection warnings, and account-ready labels without writing to the platform or changing local/offline save behavior.

Archive and Card Summary eligibility paths now route through the shared verdict model, so user-facing conflict labels are consistent across the assignment surfaces.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SharedCompanionAssignmentEligibilityBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SharedCompanionAssignmentEligibilityBuilder.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SharedCompanionAssignmentConflictModelTest.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SharedCompanionAssignmentConflictModelTest.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SystemConsoleTestRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.UnityBridge.Tests.csproj`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-shared-companion-conflict-model-slice-report.md`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed.
  - Existing warnings remained:
    - `WorldMapSurfaceBuilder.cs(649,24): warning CS0649: FoldedContributorGlyphs is never assigned`
    - `UIShellBootstrap.cs(370,22): warning CS0649: _craftCreateV2SummaryName is never assigned`
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` - passed with no output.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - `probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter shared_companion_assignment_conflict_model` - exited 0 with no failures emitted.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter shared_companion_assignment_conflict_model -Json` - passed, 1 total, 1 passed, 0 failed.
  - Automation warning signal was the existing unreachable-code warning in `InMemoryGameCOnfigProvider.cs(138,17)`.
- Final `status` after the test run - `probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.

## Cleanup performed

No destructive cleanup performed. Unity automation artifacts were left in place as run evidence under `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\artifacts\unity-automation\20260515-101905`.

## Risks

- This is still a local/read-only planner model. Lower-level services do not yet enforce remote platform assignment locks.
- Cached shared companion account locks remain advisory and freshness-bound until the write/lock protocol is designed and approved.
- Coverage is a focused pure precedence test, not a full visual regression pass across Archive/Card Summary.
- The project worktree was already very dirty; unrelated files were not reverted or cleaned.

## Memory-worthy notes

Unity now has a central non-mutating `SharedCompanionAssignmentConflictModel` for companion assignment prep. It establishes label/precedence behavior before any platform assignment mutation work:

1. Local invalid/wrong-role/local activity locks block first.
2. Cached account locks block after local locks.
3. Missing platform projection is a warning, not a block.
4. Account-ready companions are labeled but still assigned through local/offline flows only.

## Do not promote to memory

Do not promote temporary run artifact paths or the existing unrelated warning list. Do not treat this as platform lock enforcement; it is only the Unity-side read-only conflict model.

## Next recommended gate

Slice 8: add the final pre-mutation smoke/contract gate for linked-account assignment surfaces, or draft the remote companion lock/write protocol without enabling writes yet.
