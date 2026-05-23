# 2026-05-16 TWB Trenchworks War Agent First Slice Implementation Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

This pass touched only the live Trenchworks project at:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

It did not touch The World Beneath main Unity game, Glassroot Garden, The Alchemy Lab, TWB-Marketing, shared platform/accounts, pets, sprite-sheet automation, crafting/logistics research reports, or unrelated files.

## What changed

- Added a first-slice war agent/cell simulation under the existing `WarWorld`.
- Added `WarCell` data for the current `400 x 200` map.
- Added `WarUnit` records with faction, unit type, grid position, health, morale, ammo, state, and reason string.
- Added `WarContact` records for short-lived local contact markers.
- Added war enums for faction, unit type, unit state, and obstacle type.
- Created `10 x 10` player and enemy base zones.
- Spawned `32` above-ground units per faction inside the base zones.
- Added seeded obstacle clusters across the war field while protecting base zones and base exits from blockage.
- Added simple unit scouting:
  - one unit per occupied square,
  - no friendly overlap,
  - outward movement from base,
  - avoidance of blocked cells unless clearing,
  - per-faction scouted memory.
- Added short-range contact detection and local combat resolution using:
  - health,
  - morale,
  - ammo,
  - unit type,
  - cover/obstacle/trench state,
  - player supply score,
  - bounded seeded variance.
- Added dig-in behavior after winning local contact:
  - winning units start foxhole/trench progress on their current cell,
  - sappers and engineers dig faster,
  - player trench materials improve digging and clearing.
- Kept existing strategic compatibility fields alive:
  - front progress,
  - readiness,
  - casualties,
  - trench progress,
  - tunnel progress,
  - bombardment progress,
  - player and enemy base integrity,
  - command mission and battle log.
- Updated the war renderer to show:
  - actual units,
  - obstacles,
  - contact markers,
  - foxhole/trench cells,
  - `10 x 10` base zones.
- Updated the right-side war tracker with:
  - player/enemy unit counts,
  - active contacts,
  - player/enemy trench-cell counts,
  - obstacle count,
  - sample live unit reason strings.
- Updated the README with current war-agent prototype notes.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\README.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-agent-first-slice-implementation-report.md`

## Tests/checks run

- Source search confirmed the new war cell/unit/contact paths are present in the intended files.
- Direct Unity Roslyn compile check for `Assembly-CSharp` passed with exit code `0`.
- Unity batch smoke test passed:

```powershell
Unity.exe -batchmode -quit -projectPath C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest
```

Smoke result from the Unity log:

```text
TWB Trenchworks smoke test passed. First shipment tick: 45. First front gain tick: 369. Final front: 100.0. Enemy base: 0.0.
```

## Cleanup performed

- Removed temporary compile/smoke output folder:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\CodexCompileCheck
```

- Verified that temporary folder was removed.
- Did not edit Obsidian `memory/wiki`, `memory/index.md`, `memory/hot.md`, or `memory/log.md`.

## Risks/open questions

- The old strategic front/bombardment summary still coexists with the new agent layer. This is intentional compatibility for the first slice, but later work should make the strategic summary derive more fully from the unit/cell model.
- Unit movement is deliberately simple and local; it is not full pathfinding.
- The map is `80,000` cells, so future larger unit counts should avoid full-map work per unit per tick.
- Contact/combat is readable but still crude. It needs balancing after visual playtesting.
- Obstacles are seeded and clearable, but corridor validation is still basic rather than a full flood-fill guarantee.
- Unit reason strings are present but not yet selectable per unit/cell.
- The war can still resolve through the legacy bombardment smoke path before the agent layer alone could organically annihilate the enemy base.

## Follow-up recommendations

- Add click/hover inspection for war cells and units.
- Add a dedicated overlay button for scouted/unknown cells.
- Replace the old front-progress source with a derived control/front calculation once agent movement and contact feel good.
- Add pure C# tests for base placement, obstacle generation, unit occupancy, scouting, local contact, and dig-in.
- Add lightweight pathfinding or sector routing before increasing unit counts.
- Make bombardment readiness depend on captured/held sectors, trench network, and supply reach rather than only the compatibility front value.

## Anything blocked

Nothing blocked. Unity batchmode was available and the smoke test passed.
