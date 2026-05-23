# TWB Trenchworks Live Integration Pass Report

Date: 2026-05-16

Scope: standalone Unity 2D game under The World Beneath umbrella.

## What changed

- Killed the Hubble/Descartes heartbeat and decommissioned both finished workers before starting the single integration pass.
- Added a live integration bridge that owns the prototype catalog, production facade, research facade, and team-war facade.
- Wired the integration bridge into `TrenchworksSimulation` so it ticks alongside the current prototype loop.
- Added visible UI hooks in Play mode:
  - top-bar research point count,
  - right-side Research tracker with Tier 1 production and war research purchase buttons,
  - integrated production diagnostics in the Logistics tracker,
  - integrated team-war diagnostics in the War tracker,
  - integration event log in the Log tracker,
  - war-bottom team spawn buttons for scout, assault, engineer, and supply teams,
  - map overlay for integrated team members, contacts, and trench-network plans.
- Extended the editor smoke menu to run the integrated production/research/team-war smoke check after the legacy prototype smoke.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\IntegratedPrototypeSystems.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-live-integration-pass-report.md`

## How to run it in Unity Hub

1. Open Unity Hub.
2. Open project folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open or confirm scene: `Assets\Scenes\TrenchworksPrototype.unity`.
4. Press Play.
5. Use the bottom-left circle to toggle Factory/War.
6. In War view, use the bottom row for doctrine, entry lane, team spawns, and layers.
7. Use the right Tracker panel:
   - `RES` buys Tier 1 research,
   - `WAR` shows team-war state,
   - `LOGI` shows production/research production diagnostics,
   - `LOG` shows battle/factory/integration logs.

## Whether `prototype\My project` was involved

Not involved. This pass only touched the current canonical project home:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

No nested `My project` folder was used or deleted.

## Tests/checks run

- Runtime Unity source compile via generated Roslyn response file: passed.
- Editor Unity source compile via generated Roslyn response file with fresh runtime ref: passed.
- Temporary no-window smoke runner against the same source set: passed.

Smoke output:

```text
integrated smoke passed=True, ready=True, rp=972, completed=6, teams=2, productionRp=2
prototype ticks=3000, shipments=448, rp=92
```

## Cleanup performed

- Deleted the recurring heartbeat `check-trenchworks-hubble-descartes`.
- Closed/decommissioned Hubble and Descartes after their work completed.
- Temporary compile and smoke directories were removed:
  - `Temp\CodexCompileCheck`
  - `Temp\CodexSmokeCheck`

## Risks

- The legacy strategic war loop and the new team-war facade currently coexist. The UI now exposes both, but final gameplay should eventually choose one authoritative war model.
- The open Unity Editor log still contained stale compile errors from before the final fixes. The generated source compile and smoke runner pass; Unity may need to refresh/recompile when the editor regains focus.
- Team spawn buttons are prototype-level: they call the new team facade and display results, but they do not yet debit the production inventory by team resource cost.
- Research purchase UI is intentionally Tier 1 only for this pass.

## Memory-worthy notes

- The integration bridge pattern works: production-generated research points are imported into the research facade, completed war research unlocks are applied into the war-team facade, and team spawns become visible on the map.
- The team-war prototype now has a live path from research unlocks to player-spawned teams and dynamic trench-network plan rendering.
- The canonical Unity Hub project remains `TWB-TrenchWorks`, not the destroyed/old prototype location.

## Follow-up recommendations

- Force a Unity Editor refresh/recompile, then run `TWB Trenchworks/Run Simulation Smoke Test` from the Unity menu.
- Replace the legacy CXR/front-progress line with the team-war facade once the team model has enough behavior and supply debiting.
- Add production-cost checks for spawning teams so research unlocks and actual factory outputs both matter.
- Expand the research tracker beyond Tier 1 after Tier 1 proves readable in play.

## Anything blocked

- Full Play Mode GUI verification inside the already-open Unity Editor was not automated from Codex. Source compile and no-window smoke passed; the remaining check is pressing Play in the open editor after Unity refreshes.
