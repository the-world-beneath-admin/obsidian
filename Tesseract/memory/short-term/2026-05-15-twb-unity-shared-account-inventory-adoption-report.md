# TWB Unity Worker Report - 2026-05-15 - Shared Account Inventory Adoption

## Task

Adopt the prepared shared online account inventory into the main Unity game's archive flow so linked accounts no longer see the old local placeholder starter pets. Keep the slice narrow: load cloud-owned inventory/pet data into Unity's runtime cache for display and gameplay selection, while continuing to block unsafe local writes back to shared account inventory.

## Result

Implemented the first linked-account inventory adoption slice.

Linked account sessions now try to apply the cached platform inventory mirror during UI/session initialization and after settings cloud sync. The platform mirror importer now projects wallet/material/card stacks and starter companion packages into the Unity runtime player inventory cache. Account-selected starter pets from the shared cloud mirror should now appear in Archive instead of the previous local placeholder trio.

The old local dungeon starter fixture is no longer seeded for linked account sessions. If a linked account has no platform inventory mirror available yet, the starter fixture is removed rather than shown as authoritative account inventory.

Remote shared-inventory mutation remains blocked. Inventory mirror adoption is treated as a local cache projection, while companion lock writes and inventory event writes still fail the pre-mutation contract.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Backend\TwbPlatformInventoryMirrorImporter.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\DungeonStarterSetService.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellSimulationHost.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SettingsSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Backend\TwbPlatformPreMutationContract.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SharedPlatformPreMutationContractGateTest.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\SystemConsoleTestRegistry.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed with 0 warnings and 0 errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status`
  - Reported `Status: probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Automation summary reported `Status: probably-clean`, `ErrorSignals: 0`, but Unity batchmode also aborted because another Unity instance already had the project open. Treat this as an editor-open compile gate, not a clean full batch compile.
  - Summary artifact: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\artifacts\unity-automation\20260515-112500\summary.txt`

## Cleanup performed

Removed the temporary standalone test file that was not included by the generated Unity test project and folded the new adoption test into the existing shared platform contract test file.

No broad cleanup, staging, revert, or generated asset deletion was performed.

## Risks

The Unity side still uses local player inventory structures as a runtime cache/projection. This is intentional for this slice, but it is not the final account-owned inventory architecture.

Cloud inventory adoption depends on the cached platform mirror being available. If startup sync fails or has not completed, linked sessions now suppress local placeholders, but the Archive may appear empty until the mirror is pulled.

Starter companion import currently resolves known starter IDs from the mirror's companion card and starter selection fields. Additional cloud companion schemas may need explicit mapping if the backend evolves.

The batch Unity compile check was blocked by an already-open editor instance, so manual/editor verification of Archive contents after account sync is still the next practical gate.

## Memory-worthy notes

Linked main-game sessions should now treat shared platform inventory as the source of truth for Archive contents. The Unity local inventory is now only a projection/cache after account link.

The old local dungeon starter fixture should be considered proof-only/offline scaffolding and should not appear for linked account sessions.

Safe shared account inventory writeback remains intentionally blocked until explicit backend mutation endpoints and game rules are approved.

## Do not promote to memory

Do not promote intermediate helper names, temporary test placement details, or the specific automation artifact path as durable design truth.

## Next recommended gate

With the Unity editor open and a linked account signed in, run a manual smoke pass:

1. Open Settings and sync cloud state.
2. Open Archive.
3. Confirm the account-selected starter pets appear.
4. Confirm Ripspnout, Knotback, and Mireturn no longer appear as default placeholders unless they are actually present in the account mirror.
5. Run the System Console shared platform and archive smoke tests if practical.
