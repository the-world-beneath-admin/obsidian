# 2026-05-16 TWB Trenchworks War Integration Facade Implementation Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

Active project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass extended only the isolated War module under:

```text
Assets\Scripts\Simulation\War\
```

No live UI, `TrenchworksSimulation`, Data, Production, Research runtime, editor, bootstrap, permanent memory, wiki, index, hot, or log files were edited.

## Context read

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-full-implementation-plan-and-wireframes.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-team-scenarios-diagnostics-implementation-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-unlock-effects-implementation-report.md`
- Existing isolated module under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\`

## What changed

- Added `WarIntegrationFacade` as a stable pure-C# adapter around the existing isolated team/unlock systems.
- Added integration state/config/result classes:
  - `WarSubsystemConfig`
  - `WarSubsystemState`
  - `WarSubsystemSnapshot`
  - `WarTickResult`
- Added command/result objects:
  - `WarCommand`
  - `SpawnTeamCommand`
  - `SetEntryLaneCommand`
  - `ApplyWarResearchUnlockCommand`
  - `WarDoctrineCommand`
  - `WarCommandResult`
- Added UI/save-friendly snapshot DTOs for:
  - teams
  - team members
  - entry lane availability
  - team template availability
  - active contact samples
  - trench plans
  - diagnostics
  - pressure
  - base threat
  - bombardment readiness
- Added aggregate diagnostic snapshot output for:
  - command handling
  - team diagnostics
  - decision reasons
  - research unlock/lock reasons
- Added `WarIntegrationFacadeSmoke.RunPrototypeSmoke()` to prove:
  - locked spawn rejection
  - research unlock command handling
  - entry lane command handling
  - team spawn command handling
  - ticking produces decisions
  - snapshot includes teams, availability, lanes, diagnostics, pressure, and bombardment readiness.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarIntegrationFacade.cs.meta`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-integration-facade-implementation-report.md`

## Tests/checks run

- Checked project status; target Unity project is not a git repository.
- Compiled with Unity's Roslyn response file plus isolated War sources:

```powershell
mono.exe csc.exe @Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp Assets/Scripts/Simulation/War/WarTeamEntities.cs Assets/Scripts/Simulation/War/WarTeamSlice.cs Assets/Scripts/Simulation/War/WarTeamScenariosDiagnostics.cs Assets/Scripts/Simulation/War/WarUnlockEffects.cs Assets/Scripts/Simulation/War/WarUnlockSmoke.cs Assets/Scripts/Simulation/War/WarIntegrationFacade.cs -out:Assets/Scripts/Simulation/War/CodexCompileCheck.dll -refout:Assets/Scripts/Simulation/War/CodexCompileCheck.ref.dll -pdb:Assets/Scripts/Simulation/War/CodexCompileCheck.pdb
```

Result: compile exited `0`.

The standalone response-file invocation emitted the same Unity source-generator analyzer load warnings seen in prior passes. No C# compile errors were reported.

- Ran a disposable smoke runner against:
  - `WarTeamSmoke.RunAllPrototypeSmokes()`
  - `WarUnlockSmoke.RunPrototypeSmoke()`
  - `WarIntegrationFacadeSmoke.RunPrototypeSmoke()`

Smoke result summary:

```text
teamSmoke scout_probe passed=True teams=2 decisions=2
teamSmoke assault_no_mans_land passed=True teams=2 decisions=2
teamSmoke fortify_after_contact passed=True teams=2 decisions=2
teamSmoke supply_under_pressure passed=True teams=3 decisions=3
teamSmoke trench_connect_back_to_base passed=True teams=3 decisions=3
unlockSmoke passed=True lockedTeam=True unlockedTeam=True lockedEmplacement=True unlockedEmplacement=True entryLane=True upgraded=True
facadeSmoke passed=True lockedSpawn=True unlocks=True spawn=True decisions=True teams=True availability=True diagnostics=True
facadeSnapshot tick=4 selectedLane=Bottom teams=1 lanes=3 availability=4 diagnostics=22 pressure=2 bombardment=0
```

## Cleanup performed

- Removed temporary smoke runner source:

```text
Assets\Scripts\Simulation\War\CodexFacadeSmokeRunner.cs
```

- Removed temporary compile/smoke outputs:

```text
Assets\Scripts\Simulation\War\CodexFacadeSmokeRunner.exe
Assets\Scripts\Simulation\War\CodexFacadeSmokeRunner.pdb
Assets\Scripts\Simulation\War\CodexCompileCheck.dll
Assets\Scripts\Simulation\War\CodexCompileCheck.ref.dll
Assets\Scripts\Simulation\War\CodexCompileCheck.pdb
```

- Confirmed no `CodexFacadeSmokeRunner` or `CodexCompileCheck` artifacts remain under `Assets\Scripts\Simulation\War`.

## Risks

- The facade is intentionally not live-wired. It does not mutate `TrenchworksSimulation` or the current UI.
- Snapshot fields such as pressure, base threat, and bombardment readiness are adapter-level summaries, not final balance formulas.
- Commands use local strings/enums for stability while Hubble/Descartes integration remains in parallel. Parent integration should map catalog/research ids into these commands explicitly.
- Active contacts are currently derived from recent decision influence samples rather than a full contact-map enumeration.

## Memory-worthy notes

- Future integration can call `WarIntegrationFacade.ApplyCommand(...)`, `Tick(...)`, and `BuildSnapshot()` without reaching into team/unlock internals.
- UI can consume `WarSubsystemSnapshot` for teams, lanes, availability, contacts, trench plans, supply, diagnostics, pressure, and bombardment readiness.
- Locked/unlocked research reasons are already included in snapshot diagnostics and availability DTOs.
- Existing war scenario and unlock smoke APIs still pass alongside the new facade smoke.

## Next integration recommendation

Parent integration should first add an editor smoke method that constructs `WarIntegrationFacade.CreatePrototype()`, applies a small set of research unlock commands, spawns a team, ticks, and asserts the snapshot has teams, availability, and diagnostics. Only after that smoke path is stable should `TrenchworksSimulation` begin owning a facade instance or translating live UI actions into `WarCommand` objects.

## Anything blocked

Nothing blocked.
