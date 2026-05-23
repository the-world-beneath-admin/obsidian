# 2026-05-16 TWB Trenchworks Research Runtime Prototype Implementation Report

## Scope

Standalone TWB-tagged game: TWB Trenchworks.

Active Unity project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass implemented an isolated research runtime prototype only. It was not wired into the live UI, live simulation, Data/catalog layer, Production layer, War layer, editor setup, or bootstrap.

The project operating rules normally ask for a current game-dev brief update before meaningful work. This worker did not update that brief because the bounded task's owned write set allowed only `Assets\Scripts\Simulation\Research\` plus this short-term report.

## What changed

- Added a new isolated namespace:

```text
TWB.Trenchworks.Simulation.Research
```

- Added generic shared Research Point runtime state.
- Added two research spend domains:
  - Production.
  - War.
- Added three playable research tiers:
  - Tier 1.
  - Tier 2.
  - Tier 3.
- Added hard-coded prototype Production and War research trees based on the research-tree design report.
- Added prerequisites, capstone nodes, tier unlocks, and unlock id tracking.
- Added purchase diagnostics for:
  - unknown node,
  - already researched,
  - tier locked,
  - missing prerequisite,
  - not enough research,
  - successful purchase.
- Added validation for:
  - missing prerequisites,
  - missing capstones per domain/tier,
  - invalid capstone tier unlocks,
  - prerequisite cycles.
- Added deterministic smoke helper that proves:
  - generic RP can be granted,
  - a Tier 1 Production node can be purchased,
  - a Tier 2 Production node fails before capstone,
  - a Production capstone unlocks Tier 2,
  - a Tier 2 Production node can then be purchased,
  - the same locked/capstone/unlock flow works for War,
  - unlock ids are marked after purchases.

## Files touched

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchTypes.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchRuntimeState.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchTreeFactory.cs
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\Research\ResearchRuntimeSmoke.cs
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-runtime-prototype-implementation-report.md
```

No files under `Assets\Scripts\Data\`, `Assets\Scripts\Simulation\Production\`, `Assets\Scripts\Simulation\War\`, `TrenchworksSimulation.cs`, `PrototypeBootstrap.cs`, or editor setup were edited by this worker.

## Tests/checks run

Read required context:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-research-tree-design-report.md
```

Read project orientation:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md
```

Inspected current source layout under:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts
```

Confirmed `Assets\Scripts\Simulation\Research\` did not exist before this pass.

Compiled with Unity's generated Roslyn response file plus the new Research sources:

```powershell
dotnet exec "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll" `
  "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp" `
  "Assets\Scripts\Simulation\Research\ResearchTypes.cs" `
  "Assets\Scripts\Simulation\Research\ResearchRuntimeState.cs" `
  "Assets\Scripts\Simulation\Research\ResearchTreeFactory.cs" `
  "Assets\Scripts\Simulation\Research\ResearchRuntimeSmoke.cs" `
  "/out:Temp\CodexResearchCompile.dll" `
  "/refout:Temp\CodexResearchCompile.ref.dll"
```

Result: passed with exit code `0`.

Ran direct pure C# smoke invocation through PowerShell `Add-Type`:

```powershell
[TWB.Trenchworks.Simulation.Research.ResearchRuntimeSmoke]::RunDeterministicSmokeSummary()
```

Smoke result:

```text
research smoke passed=True, valid, RP=572, completed=16, unlocks=40, productionTier=Tier2, warTier=Tier2, steps=23
```

Key smoke confirmations:

- `prod.t1.worker_muster` purchased successfully.
- `prod.t2.basic_conveyors` failed with `TierLocked` before Production Tier 1 capstone.
- `prod.t1.capstone` purchased and unlocked Production Tier 2.
- `prod.t2.basic_conveyors` purchased after capstone.
- `war.t1.team_muster` purchased successfully.
- `war.t2.cover_posture` failed with `TierLocked` before War Tier 1 capstone.
- `war.t1.capstone` purchased and unlocked War Tier 2.
- `war.t2.cover_posture` purchased after capstone.
- `transport.basic_conveyor` unlock was present.
- `system.cover_posture` unlock was present.

Checked project git status:

```text
fatal: not a git repository (or any of the parent directories): .git
```

## Cleanup performed

Removed temporary compile outputs from project `Temp`:

```text
Temp\CodexResearchCompile.dll
Temp\CodexResearchCompile.ref.dll
Temp\CodexResearchCompile.pdb
```

Confirmed `Temp\CodexResearchCompile.dll` no longer exists.

No screenshots, throwaway logs, or scratch source files were retained.

Unity was not launched, so Unity did not generate a `Research.meta` folder file during this pass.

## Risks

- The runtime is intentionally isolated and not integrated into catalog validation, build menus, team spawn UI, save/load, or the live simulation.
- Unlock ids are strings. Some point at current catalog ids, while others are future placeholders such as `system.base_bombardment`, `unit.trench_lieutenant`, and `transport.steam_cart`.
- Tier 3 capstones are modeled as capstones but do not unlock Tier 4 yet, because the current implementation target is three playable tiers.
- Research buildings are not simulated yet. This pass models point pool and purchase/unlock runtime only.
- Other workers have recently modified Data, Production, and War files. This pass deliberately did not touch those areas.

## Memory-worthy notes

- Research runtime now exists as an isolated pure C# module under `Assets\Scripts\Simulation\Research`.
- The shared generic RP pool is implemented and verified through smoke.
- Capstone-gated tiers are implemented per domain, so Production and War tier progression can diverge.
- Purchase diagnostics are suitable for future UI tooltips and locked-button explanations.
- The prototype tree currently includes the full three-tier Production and War research plan from the design report, not only the minimal Tier 1 subset.

## Next integration recommendation

Parent integration should keep this module isolated until Hubble's Data/catalog surface, Ptolemy's Production research-building source, and Cicero's War unlock consumers are ready.

Recommended next narrow integration step:

1. Add a Data/catalog adapter or validation layer that compares research unlock ids against known catalog ids and accepted placeholder ids.
2. Add save/load serialization for `ResearchRuntimeState`.
3. Add one non-live integration test or editor smoke that calls `ResearchRuntimeSmoke.RunDeterministicSmoke()`.
4. Only after that, let UI query research state to lock or unlock build/team buttons. Do not let UI mutate research state directly; it should issue purchase commands.

## Anything blocked

Nothing blocked.
