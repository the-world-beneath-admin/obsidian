# TWB Trenchworks Trench Network Supply Field Map Report

## Scope

Standalone TWB-tagged Unity 2D prototype at:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

This continues the `War Team Authority And Frontline Field Maps` milestone. It does not touch the main TWB Unity game, The Garden, Alchemy, marketing, shared accounts, or sprite automation.

## What Changed

- Added trench network metadata to visible `WarWorld` trench cells:
  - `TrenchNetworkId`
  - `TrenchSupplyConnected`
- Added network assignment when new trench pieces are stamped:
  - new pieces connected to an open connector inherit that trench network
  - first isolated pieces get a new network id
  - adjacent supplied trench cells can mark the new piece as supply-connected
- Added simple supply-source detection around each faction entry zone.
- Added supply propagation across all active cells in the same trench network once a network connects to supply.
- Updated field-map sampling so supplied trench networks increase:
  - trench safety
  - supply reach
  - squad confidence
- Added `FieldMapSummary` to `WarUnit` so selected units expose field-map reasoning in the UI.
- Added a visible supply strip to supply-connected trench cells, so supplied networks can be seen on the war map.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-trench-network-supply-fieldmap-report.md`

## How To Run It In Unity Hub

1. Open Unity Hub to `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
2. Open `Assets\Scenes\TrenchworksPrototype.unity`.
3. Press Play.
4. Watch war trench cells after fighting/digging begins:
   - regular trench cells remain trench-colored
   - supply-connected trench cells get a thin greenish supply strip
5. Select a unit and read the right-hand selected-unit text for field-map values: cover, danger, contact heat, supply, trench safety, and blob pressure.

## Whether `prototype\My project` Was Involved

No. The obsolete nested sample project was not used or touched.

## Tests / Checks Run

- Direct Unity Roslyn compile from the live project passed with no output:

```powershell
& "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\NetCoreRuntime\dotnet.exe" exec "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll" /nostdlib /noconfig /shared "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp" "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp2"
```

- `dotnet build TWB-TrenchWorks.sln` passed with the known Unity solution warning: `Unable to find a project to restore`.
- Source scan confirmed no remaining `) switch` expression in `TrenchworksSimulation.cs`.
- Unity batch smoke was not launched because the Unity editor is already open interactively on the project.

## Cleanup Performed

- No temporary files or screenshots were created.
- No obsolete project folders were modified.

## Risks

- This is still a prototype-level network model. It uses active trench cells and simple network ids, not a full graph/path validation system.
- Supply connection currently propagates across cells sharing a network id; it does not yet model destroyed/cut communication trenches splitting a network.
- The open Unity editor log is still showing an old stale compile error from before the `% switch` cleanup. Direct source-level Unity Roslyn compile passes, so the editor likely needs to refresh/reimport or restart.

## Memory-Worthy Notes

- Trench cells now have enough metadata for future AI decisions to distinguish unsupported forward death-pockets from supplied defensive networks.
- Field-map reasoning is now visible at the selected-unit level, which is important for tuning the organic AI loop.
- The next AI pass should use `TrenchSupplyConnected` to make unsupported squads call for connection/resupply or pull back instead of simply holding forever.

## Follow-Up Recommendations

- Live-test whether supply strips become visible once trenches connect back toward entry zones.
- Add a squad-level rule: if holding a trench with poor supply reach, request engineers/supply or fall back after a timeout.
- Later replace the simple network id approach with a proper trench graph that can split when links are destroyed.

## Anything Blocked

- Live Play Mode verification remains a user/editor task because the editor is open; source compile is clean.
