# TWB Trenchworks Organic War Movement Report

## Scope

Standalone TWB Trenchworks Unity prototype at:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass did not touch the main TWB Unity project, Glassroot Garden, Alchemy Lab, marketing, shared-platform, or sprite-sheet lanes.

## What changed

- Diagnosed why the visible war test still looked like two blobs charging:
  - weapon/contact range was effectively too short;
  - scout scoring strongly rewarded straight outward movement;
  - contact handling dug only after a tidy winner/loser result;
  - completed trenches did not make units stay and defend.
- Added separate weapon and awareness ranges so rifle units begin fighting at range rather than waiting for adjacency.
- Reduced straight-line scouting pressure and added more lateral scouting/cover/crowding considerations.
- Added standoff movement so units approach rifle range while looking for cover instead of always closing to melee distance.
- Changed combat digging semantics:
  - a unit that gains a clear combat edge starts digging in;
  - engineers and sappers in or near the fight dig under fire to provide cover;
  - combat does not require a final binary winner before entrenchment begins.
- Changed completed trench behavior:
  - once a unit completes a friendly trench/foxhole, it enters a holding/defending state;
  - units in completed friendly trenches do not resume pushing forward unless an enemy comes into weapon range.
- Preserved the current wave-drill test and did not wire in the queued squad-spawn UI.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-organic-war-movement-report.md`

## Tests/checks run

- Unity/Roslyn source compile using the project `Assembly-CSharp.rsp`: passed.
- No-window organic war AI smoke: passed.
  - `waves=4/4`
  - `units=80/80`
  - `contacts=1`
  - `trenches=0/1`
  - `heldTrench=True`
  - `playerLanes=3`
  - `enemyLanes=3`
  - `playerYSpan=457`
  - `seconds=374`
- Full Unity batchmode was not run because the live Unity editor still owns `Temp\UnityLockfile`.

## Cleanup performed

- Removed `Temp\CodexCompileCheck`.
- Did not write to Obsidian wiki/index/hot/log.
- Did not touch the old `prototype\My project` sample project.

## Risks

- This is still prototype AI, not the final team/squad doctrine system.
- Units now hold completed trenches, which may make the war feel more static until player-spawned squads, artillery, lane supply, or orders are wired in.
- The smoke proves the behavior can happen deterministically, but live visual tuning may still be needed for how often trenches appear and how fast firefights develop.
- The current Play Mode drill still starts from `StartWarWaveDrillOnPlay`; after visual review it should become a debug toggle or menu item.

## Memory-worthy notes

- Fact - Legacy `WarWorld` now supports ranged fire, standoff movement, and combat entrenchment.
- Fact - Clear combat edge now starts trench digging; a complete trench causes the unit to hold and defend.
- Fact - Engineers/sappers near combat provide mid-fight digging support.
- Warning - Holding trenches is now intentionally sticky; future attack behaviour should come from new squads/orders rather than individual units wandering forward from completed cover.

## Follow-up recommendations

- Add a debug overlay/count for units in `Scouting`, `Fighting`, `DiggingIn`, and `Holding`.
- Add a temporary squad-spawn UI after this behavior is visually accepted, using the queued note from `2026-05-16-twb-trenchworks-squad-spawn-ui-queued-note.md`.
- Next AI pass should connect team identity and orders so assault teams push, scouts probe, engineers fortify, and supply teams avoid combat.

## Anything blocked

Full Unity batchmode remains blocked while the live editor has the project open. Source-level compile and deterministic no-window AI smoke passed.

## Addendum - Looping Squad Pulse Drill

### What changed

- Changed the big war-wave Play Mode drill from one oversized starter clash into a looping squad-pulse drill.
- The drill now clears the legacy starter units before it begins.
- On drill start, TOP, MIDDLE, and BOTTOM spawn points each emit one 4-unit squad for the player and one 4-unit squad for the enemy.
- The drill pulses every 15 strategic seconds for 4 pulses, then waits 30 strategic seconds and begins the next cycle.
- The drill remains active indefinitely for mass-scale observation instead of ending after a fixed wave count.
- Updated the in-game drill status text to show cycle, pulse-in-cycle, total pulses, and time until next pulse.
- Updated the editor smoke test expectations from finite waves to looping pulses.

### Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-organic-war-movement-report.md`

### Tests/checks run

- Unity/Roslyn source compile using the project `Assembly-CSharp.rsp`: passed.
- No-window looping wave-drill smoke: passed.
  - `pulses=21`
  - `cycle=6`
  - `units=504`
  - `contacts=1`
  - `trenches=1`
  - `next=4s`

### Cleanup performed

- Removed `Temp\CodexCompileCheck`.
- Did not wire the separate manual squad-spawn UI into the running game.
- Did not write to Obsidian wiki/index/hot/log.

### Risks

- The loop intentionally accumulates units over time. This is useful for stress-viewing the war AI, but long live-editor sessions may become heavy until a drill cap or cleanup toggle is added.
- The current drill squad size is 4 units per spawn point per side per pulse.
- Unity editor menu smoke was not launched because Unity is already open on the project; a second batch-mode editor can fight the project lock.

### Memory-worthy notes

- Fact - The mass-scale war drill now uses lane-based recurring reinforcement pulses rather than one big initial blob.
- Fact - Each side gets TOP/MIDDLE/BOTTOM squads on the same cadence, which should make lane behavior easier to observe.
- Warning - The drill is deliberately infinite and should stay a debug/playtest mode, not the final campaign spawn model.

### Follow-up recommendations

- Add a visible drill toggle/cap before leaving this as a default Play Mode experience.
- Add lane-by-lane pulse counters if the right-side unit summary becomes crowded.
- After visual review, wire the separate manual squad-spawn UI without interrupting this drill.
