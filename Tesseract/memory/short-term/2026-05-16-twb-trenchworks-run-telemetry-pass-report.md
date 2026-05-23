# TWB Trenchworks Run Telemetry Pass Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D prototype.

## What changed

- Added an automatic war run telemetry recorder to the Unity prototype bootstrap.
- The recorder starts on scenario reset / Play startup, samples once per strategic second, and writes a CSV plus a rolling Markdown summary.
- Added a tiny top-bar telemetry counter while the war view is active, so the player can tell the recorder is running.
- Added `QuietContactSeconds` as a public simulation metric so telemetry can flag quiet-front stalls.
- The recorder watches for likely holes in the war loop with flags:
  - `OK`
  - `QUIET_FRONT`
  - `CONTACT_NO_PROGRESS`
  - `NO_MATERIAL_CHANGE`
  - `VICTORY`
  - `FORCE_COLLAPSE`

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-run-telemetry-pass-report.md`

## How to run it in Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. Open or use `Assets\Scenes\TrenchworksPrototype.unity`.
3. Press Play.
4. Let the wave drill run for several minutes.
5. Read the latest files under:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Logs\Telemetry
```

Expected outputs:

- `war-run-YYYYMMDD-HHMMSS.csv`
- `war-run-YYYYMMDD-HHMMSS-summary.md`

The CSV records population, deaths, fighting/digging/holding/scouting counts, commandless troops, suppression, low ammo, active contacts, grenade contacts, quiet-contact time, material-change time, front progress, base integrity, trench cells, supplied/isolated trench networks, active/static simulation units, and the current watch flag.

The Markdown summary updates every 10 telemetry samples and again when Play stops, resets, or the bootstrap disables.

## Whether `prototype\My project` was involved

No. This pass only touched the new canonical project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

## Tests/checks run

- Read the required current memory context:
  - `memory/hot.md`
  - `memory/index.md`
  - `memory/wiki/game-dev/project-hierarchy.md`
- Ran source-level solution check:

```powershell
dotnet build "C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln"
```

Result: passed with the existing warning that no restore project was found.

- Ran Unity Roslyn compile against the current Bee response files:

```powershell
& "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\NetCoreRuntime\dotnet.exe" exec "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll" /nostdlib /noconfig /shared "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp" "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp2"
```

Result: passed.

- Checked the live Unity editor log. The editor was open, but its log timestamp was older than the telemetry patch, so the currently running editor had not yet imported the new recorder during this check.
- Checked for existing `Logs\Telemetry` output. No telemetry folder existed yet because Unity had not imported and run this patch at the time of inspection.

## Cleanup performed

- No temporary files were created for this pass.
- No nested project folders were deleted or modified.

## Risks

- The live editor must refresh/import scripts before the recorder appears in-game.
- Because telemetry samples by strategic second, paused play does not add new samples.
- Current stall flags are intentionally coarse. They are meant to point Bob and future workers toward suspicious run windows, not prove root cause by themselves.
- CSV row counts may grow during very long sessions, though this is acceptable for prototype-scale diagnostics.

## Memory-worthy notes

- The war loop now has a run-observation surface: CSV plus rolling summary.
- `CONTACT_NO_PROGRESS` is the main flag to inspect for cover/trench stalemates.
- `QUIET_FRONT` is the main flag to inspect for teams that stop finding each other.
- `NO_MATERIAL_CHANGE` is the broad smoke alarm for long-running battlefield inactivity.
- The telemetry should be used before further large AI changes, so future changes can be compared against a known run trace.

## Follow-up recommendations

- After the next long Play session, inspect the latest `war-run-*-summary.md` first, then open the CSV around any flagged seconds.
- Add a tiny in-game "export/open latest telemetry" button later if manual file browsing becomes annoying.
- If the next run still visibly stalls, correlate `active_contacts`, `fighting`, `grenade_contacts`, `seconds_since_material_change`, and `trench network` columns before changing combat again.
- Consider adding per-team order samples later, but only after the current whole-run telemetry proves which questions remain unanswered.

## Anything blocked

- Live Unity verification of generated telemetry files was blocked because the open editor had not imported the newer source patch by the time checks were run.
- Batchmode Unity smoke testing was skipped because the Unity editor was already open on the project.
