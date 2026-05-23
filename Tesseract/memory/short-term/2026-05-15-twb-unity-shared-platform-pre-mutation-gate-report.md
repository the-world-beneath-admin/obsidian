# TWB Unity Worker Report - 2026-05-15 - Shared Platform Pre-Mutation Gate

## Task

Complete slice 8 of 8 for the main Unity game/shared platform integration: add a conservative pre-mutation gate so linked-account assignment surfaces remain local/read-only until shared companion and inventory mutation is explicitly designed.

## Result

Added a Unity-side `TwbPlatformPreMutationContract` that distinguishes permitted pre-mutation operations from blocked shared companion/inventory mutation operations. Device link, account state pull, cloud save read/write, profile snapshot record, and local assignment prep are allowed. Companion lock create/refresh/release, inventory event writes, and platform inventory adoption into the main-game profile remain blocked.

Added a focused System Console gate that validates the contract and scans the Card Summary / shared companion assignment builders for platform write calls or blocked inventory-event endpoint tokens.

Settings now states the operational boundary directly: account pulls may read exported/shared state, assignment is local-only, and no companion lock writes occur.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Backend\TwbPlatformPreMutationContract.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Backend\TwbPlatformPreMutationContract.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SharedPlatformPreMutationContractGateTest.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SharedPlatformPreMutationContractGateTest.cs.meta`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SystemConsoleTestRegistry.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SettingsSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.UnityBridge.csproj`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.UnityBridge.Tests.csproj`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` - passed. Existing warnings: `WorldMapVisualStackStats.FoldedContributorGlyphs` unused/default and `_craftCreateV2SummaryName` unused/default.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` - passed.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` - passed, `Status: probably-clean`, no error or warning signals.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-systemconsole -TestFilter shared_platform_pre_mutation_contract_gate -Json` - passed, 1/1 tests passed. Automation summary reported one existing warning: `Assets\_TWB\Scripts\Services\Config\InMemoryGameCOnfigProvider.cs(138,17): warning CS0162: Unreachable code detected`.
- Final status check after the narrow console run - passed, `Status: probably-clean`, no error or warning signals.

## Cleanup performed

No throwaway scratch files were created. Unity generated `.meta` files for the new source files and they were retained as required project assets. Unity automation artifacts were retained as verification evidence.

## Risks

The new gate is intentionally conservative: it prevents Unity from writing shared companion locks or inventory events, but it does not implement the eventual platform mutation protocol. Assignment remains local/offline and platform locks remain advisory/read-only.

`SettingsSurfaceBuilder.cs` is currently untracked in this worktree despite being part of the active UI surface; this report treats it as touched because the settings text was updated there. Do not use blanket git cleanup.

## Memory-worthy notes

Unity now has a named pre-mutation contract for the shared platform work. The current boundary is: account state can be pulled, profile/cloud-save operations can continue, and assignment prep can read cached account companion/lock data, but Unity must not write companion locks, inventory events, or adopt platform inventory into the main-game profile.

## Do not promote to memory

Do not promote the transient Unity automation artifact paths or the exact warning counts. The durable note is the pre-mutation boundary, not the run directory.

## Next recommended gate

Bob/orchestrator should decide whether the next gate is a real shared companion mutation design pass. That should start with the backend event contract, idempotency/conflict model, lock lifetime policy, and explicit Unity offline fallback before any remote write is added.
