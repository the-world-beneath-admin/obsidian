# TWB Unity Worker Report - 2026-05-15 - Account Persistence Safety Slice

## Task

Proceed with the first implementation step from the account/inventory persistence plan: make the prepared platform inventory mirror safe for the main Unity game before deeper persistence wiring.

Scope: Main game / The World Beneath, with shared platform/account integration.

## Result

Completed the first safety slice.

- Settings now presents the platform pull surface as `Shared Account State`, not a mutable shared-inventory mirror.
- The settings row now offers `Pull` and `Snapshot`; the visible destructive `Adopt` action was removed.
- Snapshot/cloud-save status copy now says it records a profile snapshot and refreshes account state, rather than claiming shared inventory was uploaded/refreshed.
- Inventory V2 account panel wording now presents platform stacks as exported/read-only account state.
- `TwbPlatformInventoryMirrorImporter.ApplyToPlayer` now fails closed with a clear disabled reason before touching local Will, materials, or cards.
- `UIShellSimulationHost.AdoptPlatformInventoryMirror` also fails closed before requiring an active save or calling the importer.

No backend deploys, remote migrations, or Cloudflare production changes were performed.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-account-persistence-safety-slice-report.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Backend\TwbPlatformInventoryMirrorImporter.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Backend\TwbPlatformAccountLinkClient.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\SettingsSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\InventorySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellSimulationHost.cs`

Note: the Unity working tree was already heavily dirty before this slice. Several touched Unity files were already modified or untracked from prior work; this pass only made the account-state wording and fail-closed inventory-adoption edits described above.

## Checks run

From `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`:

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Passed.
  - Warnings: two existing unassigned-field warnings in `WorldMapSurfaceBuilder.cs` and `UIShellBootstrap.cs`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status`
  - Passed.
  - Status: `probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Returned exit code `0`.
- Post-compile status check:
  - Status: `probably-clean`, `ErrorSignals: 0`, `WarningSignals: 0`.

## Cleanup performed

No temporary scratch files were created.

## Risks

- The old destructive importer code still exists behind a disabled guard. This is intentional for now, but it should not be enabled until a real import/migration design exists.
- `sync-snapshot` still has DTO names like `platformInventory` because the website endpoint contract already uses that shape. UI wording has been corrected, but deeper contract cleanup remains a later slice.
- Unity cloud-save load still restores the cloud slot directly. Conflict handling and local backup before cloud load remain future work.
- Source event ids remain tick-based and are not retry-idempotent for a single logical snapshot operation.

## Memory-worthy notes

- Main-game Unity should treat platform inventory as read-only account state until explicit import/export contracts are designed.
- Website account state can safely be pulled for account home, shared companions, exported stacks, locks, and cloud save listings.
- Local Will/material/card inventory should remain local-first through this gate.

## Do not promote to memory

- Do not promote this whole report verbatim.
- Do not treat the disabled importer as a final architecture decision; it is a safety gate until a proper import/export design is approved.

## Next recommended gate

Proceed to the next persistence slice: cloud save guardrails.

Recommended scope:

- Add local backup before cloud load.
- Compare local save metadata against cloud slot metadata before loading.
- Make cloud load require an explicit user action when local and cloud data both exist.
- Keep account state pull and profile snapshot separate from cloud save restore.
