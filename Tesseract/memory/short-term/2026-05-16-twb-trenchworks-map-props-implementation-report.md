# TWB Trenchworks Map Props Implementation Report

Date: 2026-05-16

Scope: standalone TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This pass did not touch the main TWB Unity project, Glassroot Garden, Alchemy Lab, marketing, shared-platform, or sprite-sheet lanes.

## What changed

- Implemented the first set of simplified war-map props:
  - mud patch
  - old shell crater
  - deep shell crater
  - low earth berm
  - high earth bank
  - dry drainage gully
  - stone outcrop
  - boulder scatter
  - tall grass field
  - reed bed
  - sparse wooded area
  - dense wooded area
- Added simple terrain effect tiers to `WarCell`:
  - half/full cover
  - half/full concealment
  - normal/slow/very slow movement
  - below-ground stance allowance for craters, gullies, and trenches.
- Replaced the old tiny random obstacle seeding with a first-pass terrain prop generator.
- Play Mode now starts the war-wave drill with a randomized battlefield seed every reset/open.
- Deterministic editor/smoke paths still use `CreateWarWaveDrillScenario()` so checks remain repeatable.
- Concealment now reduces spotting range until a target is known through contact.
- Cover now reduces incoming combat damage instead of only boosting combat power.
- Slow terrain now delays unit movement into that cell.
- War map rendering now gives the new props distinct colors.
- Editor smoke checks now verify that all first-set map props are generated and that cover, concealment, and slow terrain exist.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-map-props-implementation-report.md`

## Tests/checks run

- Unity/Roslyn runtime source compile using the project `Assembly-CSharp.rsp`: passed.
- Unity/Roslyn editor source compile using `Assembly-CSharp-Editor.rsp` with the temporary runtime reference: passed.
- No-window deterministic map-props smoke: passed.
  - `propCells=32814`
  - `fullCover=3914`
  - `fullConcealment=4964`
  - `pulses=15`
  - `units=360`
  - `contacts=1`
  - `trenches=8`

## Cleanup performed

- Removed temporary compile/smoke harness under `Temp\CodexCompileCheck`.
- Did not write to Obsidian wiki/index/hot/log.

## Risks

- This is still a simulation-first prototype implementation, not final terrain art or tilemap rendering.
- Cover and concealment are now mechanically distinct, but unit posture itself is not fully implemented yet.
- Movement delay is cell-entry based and still grid-step visible; true smooth motion will need render interpolation later.
- The generator uses tuned random patch budgets, not a final map-validation pass with flood-fill route acceptance.
- Play Mode now randomizes the drill battlefield, so two presses of Play can look meaningfully different.

## Memory-worthy notes

- Fact - First-set war map props are now implemented as terrain cell effects.
- Fact - Cover reduces incoming bullet damage; concealment reduces spotting until contact reveals the unit.
- Fact - Play Mode wave drill now randomizes the war-map seed before starting the squad-pulse sequence.
- Warning - The old obstacle report is superseded by the simplified cover/concealment direction.

## Follow-up recommendations

- Add a terrain legend or hover/selection readout once visual review confirms the colors.
- Add explicit unit posture states next: surface standing, crouching, prone, below-ground standing, below-ground crouching.
- Add route validation before accepting a random war map.
- After live review, tune prop density and colors if the map looks too busy or too muted.

## Anything blocked

Full Unity batchmode/editor automation was not launched because the live Unity editor is already open on the project. Source-level runtime/editor compiles and deterministic no-window map-props smoke passed.
