# Starter Pet Testing

## Reported Checks

The intake reported these checks were run in the prior worker window:

- `dotnet build TWB.Domain.csproj --no-restore`
- `dotnet build TWB.Services.csproj --no-restore`
- `dotnet build TWB.UnityBridge.EditorTools.csproj --no-restore`
- `dotnet build TWB.UnityBridge.Tests.csproj --no-restore`
- Pillow image checks for Stanly PNG alpha and dimensions
- matte preview composites for Stanly cutout inspection

The Chuck decommission report added:

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore`
  - Result: passed, `0` warnings, `0` errors.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile`
  - Result: attempted but blocked because another Unity instance had the project open.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet`
  - Result: attempted but blocked because another Unity instance had the project open.
- Chuck PNG alpha validation with Pillow
  - Result: runtime and key-art PNGs reported as `1254x1254` RGBA with transparent corners.

## Required Next Verification

The next worker should run from:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype
```

Required after code changes:

```powershell
dotnet build TWB_Phase1_IdlePrototype.sln --no-restore
```

If practical:

```powershell
powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile
powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode test-editmode -TestFilter EphemrialSpiritStarterPet
```

If Unity test filtering differs, the worker should report the exact command used instead of guessing.

For Chuck, close or free the open Unity editor before retrying batchmode compile/edit-mode tests.

## Sources

- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-13-twb-unity-starter-pets-worker-final-decommission-report]]
- [[wiki/game-dev/build-test-commands]]
