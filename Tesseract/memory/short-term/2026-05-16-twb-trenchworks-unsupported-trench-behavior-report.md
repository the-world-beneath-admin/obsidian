# TWB Trenchworks Unsupported Trench Behavior Report

## Progress

3 of 8 planned war-AI steps completed.

Completed steps:

1. Team authority and visible squad intent bridge.
2. Supply-aware trench network metadata and field-map visibility.
3. Unsupported trench behavior: connect supply, hold, or fall back.

Next planned step:

4. Anti-stall order timeouts and quiet-front probes.

## Scope

Standalone TWB-tagged Unity 2D prototype at:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

This pass continues the war AI/frontline milestone and only touches the live Trenchworks project plus this short-term report.

## What Changed

- Added `WarSquadIntent.ConnectSupply`.
- Added `UnsupportedTrenchSeconds` to visible war units.
- Command units now detect when their squad is holding a completed friendly trench that is not supply-connected.
- Unsupported trench behavior now has escalation:
  - early: hold the trench briefly
  - after a short delay with engineers/sappers: broadcast `ConnectSupply`
  - if the unsupported trench becomes dangerous under contact: regroup/fall back instead of sitting forever
- `ConnectSupply` intent makes leaders and nearby engineers/sappers dig outward from existing trench connectors instead of merely improving the current trench patch.
- Supply-connection digging biases trench connector selection back toward the faction base, not forward into the enemy.
- Trench piece selection for supply connection starts with straight communication trench pieces.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-unsupported-trench-behavior-report.md`

## How To Run It In Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. Open `Assets\Scenes\TrenchworksPrototype.unity`.
3. Press Play.
4. Watch the right-hand unit summary for command units changing to `ConnectSupply` after they hold an unsupported trench.
5. Watch for greenish supply strips when a trench network becomes supply-connected.

## Whether `prototype\My project` Was Involved

No. The obsolete nested sample project was not used or touched.

## Tests / Checks Run

- Direct Unity Roslyn compile passed with no output.
- `dotnet build TWB-TrenchWorks.sln` passed with the known Unity solution warning: `Unable to find a project to restore`.
- Unity batch smoke was not launched because the Unity editor is already open interactively on this project.

## Cleanup Performed

- No temporary files, screenshots, or scratch logs were created.

## Risks

- `ConnectSupply` currently uses the existing connector-stamping grammar; it is not yet a full trench pathfinder.
- If a trench network lacks open connector ends, connection attempts can still fail and hold.
- Network splitting after destroyed trenches is not implemented yet.
- Live Play Mode behavior still needs visual confirmation.

## Memory-Worthy Notes

- Unsupported trench behavior is now explicit. A trench can be tactically useful but strategically brittle if not supply-connected.
- The squad intent list is beginning to reflect the desired loop: scout, contact, firing line, dig, hold, connect, retreat/regroup.
- Step 4 should address stalls where no contact is happening or squads are locked into long holds without new probes.

## Follow-Up Recommendations

- Implement anti-stall order timeout/probe logic next.
- Add simple diagnostics for unsupported networks and count of supplied versus isolated trench cells.
- Later replace simple connector bias with a proper trench graph/path planner.

## Anything Blocked

- Live Play Mode verification remains blocked from this worker because the editor is open; source compile is clean.
