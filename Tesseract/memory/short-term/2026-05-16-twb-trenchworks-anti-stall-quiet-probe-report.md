# TWB Trenchworks Anti-Stall Quiet Probe Report

## Progress

4 of 8 planned war-AI steps completed.

Completed steps:

1. Team authority and visible squad intent bridge.
2. Supply-aware trench network metadata and field-map visibility.
3. Unsupported trench behavior: connect supply, hold, or fall back.
4. Anti-stall order timeouts and quiet-front probes.

Steps left: 4.

Next planned step:

5. Trench network validation and supply-link diagnostics.

## Scope

Standalone TWB-tagged Unity 2D prototype at:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

This pass only touches the live Trenchworks project plus this short-term report.

## What Changed

- Added squad progress/stall tracking to visible war units:
  - `SquadStallSeconds`
  - `LastProgressX`
  - `LastProgressY`
  - `LastProbeSecond`
- Command units now track whether their squad has made meaningful progress.
- Squad order refreshes can now be forced by a stall timeout instead of waiting on normal cadence.
- Added quiet-front probe behavior:
  - if no contacts have happened for long enough, healthy squads can probe covered weak ground
  - if a squad stalls on an order, it can probe a new covered route
  - probe cadence is limited by `QuietFrontProbeIntervalSeconds`
- Quiet probes score forward/lateral candidates using the field-map sample:
  - cover
  - supply reach
  - trench safety
  - danger
  - blob penalty
  - seeded noise
- Updated the unit summary and selected-unit text to show command-unit stall seconds.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-anti-stall-quiet-probe-report.md`

## How To Run It In Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. Open `Assets\Scenes\TrenchworksPrototype.unity`.
3. Press Play.
4. Watch command rows in the right-hand Unit Summary.
5. Confirm command rows show `stall Ns`.
6. If the front goes quiet, watch for command units switching to `Scout` with reasons like:
   - `quiet probe: front went quiet, testing covered weak ground`
   - `order timeout: squad stalled, probing a new covered route`

## Whether `prototype\My project` Was Involved

No. The obsolete nested sample project was not used or touched.

## Tests / Checks Run

- Direct Unity Roslyn compile passed with no output.
- `dotnet build TWB-TrenchWorks.sln` passed with the known Unity solution warning: `Unable to find a project to restore`.
- Unity batch smoke was not launched because the Unity editor is already open interactively on this project.

## Cleanup Performed

- No temporary files, screenshots, or scratch logs were created.

## Risks

- Quiet probes currently use the same `Scout` intent rather than a separate displayed `Probe` intent, keeping the enum small but making the reason text important.
- The stall detector is intentionally simple: it tracks command-unit movement progress, not full squad path quality.
- Probe behavior may need tuning after visual playtest if it sends too many squads forward or not enough.

## Memory-Worthy Notes

- Holding is still allowed, but indefinite dead behavior now has a timeout path.
- The war loop now has a first version of the anti-stall toolkit recommended by GPT Pro: order timeout plus quiet-front probe.
- Step 5 should add diagnostics for supplied/unsupported trench networks so the player and developer can see whether the front is becoming a functioning network or an isolated pocket.

## Follow-Up Recommendations

- Live-test whether quiet probes break stalled fronts without turning every hold into a charge.
- Add trench network counts next: supplied networks, isolated networks, unsupported trench cells, and contested trench cells.
- Later, separate `Probe` from `Scout` if the UI needs a clearer tactical distinction.

## Anything Blocked

- Live Play Mode verification remains a user/editor task because the editor is open; source compile is clean.
