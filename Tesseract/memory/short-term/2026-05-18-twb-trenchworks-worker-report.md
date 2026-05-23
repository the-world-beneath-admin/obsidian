# TWB Trenchworks Worker Report - 2026-05-18

## Scope

Standalone TWB-tagged Unity game: TWB Trenchworks.

## Summary

This working window moved from live playtest feedback into planning the next major Phase 1 front-establishment rework. The current implementation state is stable enough to hand off to a fresh worker window. The next worker should start at Gate 1 implementation for the hidden paired front blueprint generator, using the markdown implementation plan already written under the Trenchworks docs folder.

## Work Completed

- Implemented the prior seven unit-tactics rewrite gates before this report window:
  - Gate 1 contact anti-stall and hold reasons.
  - Gate 2 multi-depth front assignment graph.
  - Gate 3 socket occupation and anti-blob behavior.
  - Gate 4 construction and hardpoint roles.
  - Gate 5 combat range, spotting, terrain, elevation, and posture.
  - Gate 6 support requests and stalled sector recovery.
  - Gate 7 legacy war-unit loop retirement.
- User playtest after those gates showed the front-establishment behavior was still wrong: the right-hand team could run off screen, the left-hand team could loiter, and neither side reliably established the middle/front before digging.
- User revised the design direction:
  - The match should start by procedurally generating hidden preferred trench-front blueprints for both sides.
  - The two trench lines should be balanced in power/fairness.
  - Units entering combat should claim pieces of that hidden line, build what they can, and defend it.
  - Phase 2 should only begin once at least one side has completed enough of its initial trench line.
  - The player should not see the hidden preferred front directly.
- Wrote detailed markdown implementation plans for the Phase 1 front-establishment rework:
  - Master plan: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-00-master-plan.md`
  - Gate 1: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-01-hidden-paired-front-blueprint-generator.md`
  - Gate 2: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-02-fairness-and-power-scoring.md`
  - Gate 3: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-03-squad-claim-allocation.md`
  - Gate 4: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-04-phase1-movement-build-priority.md`
  - Gate 5: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-05-hidden-to-visible-rendering.md`
  - Gate 6: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-06-validation-and-playtest-gates.md`
- Changed the current playtest sequence so the prototype no longer sends chunky legacy-style waves. It now:
  - Unlocks the available integrated squads and entry lanes.
  - Clears legacy war units for the playtest front drill.
  - Immediately spawns one random available integrated squad from each TOP/MID/BOT entry point for each side.
  - Repeats that random integrated squad pulse every 30 strategic seconds.
  - Caps integrated drill teams at 24 teams per faction.
- Adjusted team supply consumption so teams no longer passively burn food and construction while merely moving toward the front. Food/ammo consumption now happens only under contact pressure through the existing `ConsumeForTeam` path; construction is no longer passively drained by the timer.
- Updated UI/status text and telemetry naming to refer to the new front drill instead of the old wave drill where relevant.
- Updated simulation smoke expectations so the smoke now checks the integrated front drill shape rather than expecting old legacy war-unit wave groups.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\IntegratedPrototypeSystems.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamSlice.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\War\WarTeamTypes.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-00-master-plan.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-01-hidden-paired-front-blueprint-generator.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-02-fairness-and-power-scoring.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-03-squad-claim-allocation.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-04-phase1-movement-build-priority.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-05-hidden-to-visible-rendering.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-06-validation-and-playtest-gates.md`

## Checks Run

- Attempted Unity batchmode simulation smoke:
  - Command targeted `TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest`.
  - Log path: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-front-drill-random-squad-smoke.log`
  - Result: blocked because the Unity project was already open in another Unity instance.
- Ran `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln --no-restore`.
  - Result: passed with 0 warnings and 0 errors.
  - Caveat: this Unity solution appears effectively empty/minimal, so this is not a full substitute for Unity compilation.
- Inspected current Unity editor log after script reload.
  - No current C# compiler errors were found in the inspected tail/search.

## Current State

- Live project remains `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Canonical scene remains `Assets\Scenes\TrenchworksPrototype.unity`.
- Unity was open during the last validation attempt, so batchmode could not run.
- The current prototype start sequence now uses the integrated front drill rather than the old visible legacy war-unit wave drill.
- The Phase 1 front-establishment implementation plan is written and ready. The next worker should start at:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-01-hidden-paired-front-blueprint-generator.md`
- The master plan for sequencing and terminology is:
  - `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-00-master-plan.md`

## Risks / Fragile Areas

- The integrated front drill change has not yet passed Unity batchmode smoke because the editor was already open. Run the smoke after closing Unity or use the in-editor menu check.
- The new front drill may still need live visual review to confirm teams spread into the hidden front shape once Gate 1 exists.
- Current code still has historical names such as `CreateWarWaveDrillScenario`; some are intentionally left for compatibility, but the behavior now starts the integrated front drill.
- The next implementation must be careful not to expose hidden front blueprints visually. Only build-site claims and actual construction should become visible.
- Do not confuse the existing multi-depth assignment graph with the new user-approved requirement: a hidden paired trench-front blueprint should exist at match start and squads should claim/build pieces of it.

## Memory-Worthy Notes

- Durable user decision: Phase 1 should begin with a hidden procedurally generated paired front for both factions, not freeform squads wandering toward loose front-line assignments.
- Durable user decision: trench fronts should be balanced/fair by generated power scoring before squads begin building.
- Durable user decision: squads should claim and build random/weighted pieces of the generated front, then defend them.
- Durable user decision: player should not see the preferred/generated front directly.
- Durable user decision: Phase 2 should start after a trench line is sufficiently completed, and then focus on trench-to-trench attack behavior.
- Confirmed issue: after previous tactics gates, playtest still showed teams failing to establish the middle/front reliably.
- Confirmed fix attempt: test sequence now spawns one random available integrated squad from each entry point every 30 seconds, instead of old clustered wave behavior.
- Confirmed fix attempt: passive supply drain was reduced so squads do not run out of food/construction before reaching/building the front.

## Do Not Promote

- Do not promote assumptions that the new front drill fully fixes live behavior until Unity Play Mode visual testing confirms it.
- Do not promote exact tuning values for future front blueprint spacing/power until Gate 1 and Gate 2 are implemented and tested.
- Do not promote the current old method names as final architecture; some are compatibility leftovers.

## Cleanup Performed

- No temporary screenshots or scratch artifacts were created in this final handoff pass.
- Batchmode log `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\unity-front-drill-random-squad-smoke.log` was preserved because it documents the Unity-open blocker.
- No source files, user files, raw evidence, reports, or another worker's work were deleted.

## Next Recommended Gate

Start Gate 1 implementation:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\phase1-front-establishment-gate-01-hidden-paired-front-blueprint-generator.md`

Recommended first steps for the new worker:

1. Read the current Trenchworks brief and required memory pages.
2. Read the Phase 1 master plan and Gate 1 markdown.
3. Inspect the current integrated front plan classes under `Assets\Scripts\Simulation\War\`.
4. Implement the hidden paired front blueprint generator as a simulation-only layer.
5. Keep it hidden from renderer/UI except diagnostics/smoke.
6. Add narrow smoke coverage proving both sides receive paired, lane-aware, bounded, valid blueprint anchors.
7. Run Unity simulation smoke after closing the currently open Unity instance, or use the relevant in-editor menu check if batchmode remains blocked.
