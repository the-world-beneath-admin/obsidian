# 2026-05-16 TWB Trenchworks Research Integration Facade Implementation Report

## Scope

Standalone TWB-tagged game: TWB Trenchworks.

Active Unity project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass extended only the isolated Research module. It was not wired into `TrenchworksSimulation.cs`, UI, Data/catalog, Production, War, editor setup, or bootstrap.

The project operating rules normally ask for a current game-dev brief update before meaningful work. This worker did not update that brief because the bounded task's owned write set allowed only `Assets\Scripts\Simulation\Research\` plus this short-term report.

## What changed

- Added a stable pure-C# integration facade:
  - `ResearchIntegrationFacade`.
- Added save-friendly and UI-ready DTOs:
  - `ResearchSubsystemConfig`.
  - `ResearchSubsystemState`.
  - `ResearchSubsystemSnapshot`.
  - `ResearchTickResult`.
  - `ResearchCommandResult`.
  - `ResearchDiagnostic`.
  - domain/tier/node/capstone snapshot objects.
- Added command objects:
  - `ResearchCommand`.
  - `AddResearchPointsCommand`.
  - `PurchaseResearchCommand`.
  - `SetResearchFocusCommand`.
- Added facade diagnostics for:
  - empty tree/config errors,
  - unknown node,
  - already complete,
  - tier locked,
  - missing prerequisite,
  - not enough research,
  - successful purchase,
  - research points added,
  - focus changed.
- Added UI-ready snapshot data for:
  - shared RP pool,
  - active focus mode/domain/node,
  - available/locked/completed nodes by domain and tier,
  - capstone progress,
  - completed research ids,
  - current unlock ids,
  - unlock ids emitted this tick,
  - diagnostics,
  - suggested next nodes.
- Added `ResearchRuntimeState.LoadFromSaveData(...)` so the facade can round-trip through plain `ResearchSubsystemState` without exposing runtime internals.
- Added `ResearchFacadeSmoke` to prove command handling, snapshots, diagnostics, capstone tier unlocks, and emitted unlock ids.

## Files touched

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchRuntimeState.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchSubsystemDtos.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchIntegrationFacade.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchFacadeSmoke.cs
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-integration-facade-implementation-report.md
```

Existing Research files left functionally intact:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchTypes.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchTreeFactory.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchRuntimeSmoke.cs
```

No files under `Assets\Scripts\Data\`, `Assets\Scripts\Simulation\Production\`, `Assets\Scripts\Simulation\War\`, `TrenchworksSimulation.cs`, `PrototypeBootstrap.cs`, or editor setup were edited by this worker.

## Tests/checks run

Read required reports:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-tree-design-report.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-runtime-prototype-implementation-report.md
```

Read project orientation:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md
```

Inspected existing Research module:

```text
ResearchTypes.cs
ResearchRuntimeState.cs
ResearchTreeFactory.cs
ResearchRuntimeSmoke.cs
```

Compiled with Unity's generated Roslyn response file plus all Research sources:

```powershell
dotnet exec "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll" `
  "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp" `
  "Assets\Scripts\Simulation\Research\ResearchTypes.cs" `
  "Assets\Scripts\Simulation\Research\ResearchRuntimeState.cs" `
  "Assets\Scripts\Simulation\Research\ResearchTreeFactory.cs" `
  "Assets\Scripts\Simulation\Research\ResearchRuntimeSmoke.cs" `
  "Assets\Scripts\Simulation\Research\ResearchSubsystemDtos.cs" `
  "Assets\Scripts\Simulation\Research\ResearchIntegrationFacade.cs" `
  "Assets\Scripts\Simulation\Research\ResearchFacadeSmoke.cs" `
  "/out:Temp\CodexResearchFacadeCompile.dll" `
  "/refout:Temp\CodexResearchFacadeCompile.ref.dll"
```

Result: passed with exit code `0`.

Existing runtime smoke:

```text
research smoke passed=True, valid, RP=572, completed=16, unlocks=40, productionTier=Tier2, warTier=Tier2, steps=23
```

New facade smoke:

```text
research facade smoke passed=True, steps=12, research tick succeeded=False, commands=1, emitted=0, RP=572, completed=16, unlocks=40, emitted=0, diagnostics=1, suggestions=3
```

Note: the final tick in the facade smoke is intentionally an `UnknownNode` diagnostic check, so that individual tick reports `succeeded=False` while the overall smoke reports `passed=True`.

Facade smoke proved:

- `SetResearchFocusCommand` updates focus snapshot data.
- `PurchaseResearchCommand` without RP emits `NotEnoughResearch`.
- `AddResearchPointsCommand` updates the shared RP pool.
- Tier 2 Production purchase emits `TierLocked` before Production capstone.
- Production Tier 1 capstone chain emits `tier.production.2`.
- Production Tier 2 purchase emits `transport.basic_conveyor`.
- Already completed purchase emits `AlreadyComplete`.
- Tier 2 War purchase emits `TierLocked` before War capstone.
- War Tier 1 capstone chain emits `tier.war.2`.
- War Tier 2 purchase emits `system.cover_posture`.
- Unknown node purchase emits `UnknownNode`.
- Snapshot includes domains, capstone progress, suggestions, diagnostics, completed ids, and unlock ids.

Checked project git status:

```text
fatal: not a git repository (or any of the parent directories): .git
```

## Cleanup performed

Removed temporary compile outputs from project `Temp`:

```text
Temp\CodexResearchFacadeCompile.dll
Temp\CodexResearchFacadeCompile.ref.dll
Temp\CodexResearchFacadeCompile.pdb
```

Confirmed `Temp\CodexResearchFacadeCompile.dll` no longer exists.

No screenshots, throwaway logs, or scratch files were retained.

## Risks

- This facade is intentionally isolated and not yet authoritative for live UI/build/team locking.
- Snapshot and command DTOs use strings for ids; parent integration should validate unlock ids against Hubble's Data/catalog layer or accepted placeholders.
- `ResearchSubsystemState` is save-friendly, but no project save/load serializer has been implemented yet.
- Facade command handling is synchronous and immediate. It does not yet model research-building production ticks, active timed research, or queueing.
- Some facade snapshot lists are intentionally rich for UI exploration; live UI should select the needed subset to avoid drawing too much every frame.

## Memory-worthy notes

- The Research module now has a stable facade surface for parent integration:
  - commands in,
  - `ResearchTickResult` out,
  - `ResearchSubsystemSnapshot` for UI,
  - `ResearchSubsystemState` for save-friendly storage.
- Unlock ids emitted per tick are now explicit, so future integration can dispatch unlock effects without diffing whole state externally.
- Capstone progress snapshots exist for every domain/tier.
- Suggested next nodes are generated from tier unlock, prerequisite, cost, and completion state.
- The facade smoke now covers not-enough-RP, tier-locked, already-complete, unknown-node, capstone unlock, snapshot, and emitted-unlock flows.

## Next integration recommendation

Parent integration should wait for Ptolemy and Cicero's production/war facades, then add a thin adapter layer that:

1. Creates one `ResearchIntegrationFacade`.
2. Stores one `ResearchSubsystemState` inside the future integrated simulation state.
3. Sends only command objects into the facade.
4. Reads `ResearchSubsystemSnapshot` for UI display.
5. Applies `UnlockIdsCompletedThisTick` through narrow adapters owned by Data/Production/War rather than letting Research mutate those systems directly.

Do not wire Research directly into build placement, team spawning, or UI mutation yet. The facade is now ready for the parent to orchestrate that integration politely and with fewer sharp objects on the carpet.

## Anything blocked

Nothing blocked.
