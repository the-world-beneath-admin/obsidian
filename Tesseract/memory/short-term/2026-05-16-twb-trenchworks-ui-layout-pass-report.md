# TWB Trenchworks UI Layout Pass Report

Date: 2026-05-16
Scope: standalone TWB-tagged Unity 2D game.
Project: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## What changed

- Researched factory-builder UI layout using public Captain of Industry references plus comparable factory/management UI patterns.
- Safely checked the local Captain of Industry Steam install only for manifest/changelog/surface information. No binaries, asset bundles, saves, or proprietary assets were inspected or copied.
- Reworked the Trenchworks bottom rail from a flat tool strip into a category-first build/control rail.
- Added bottom category buttons:
  - `MAT` Materials
  - `MOV` Movement/transport
  - `MAC` Machines
  - `STM` Steam
  - `ASM` Assembler recipes
  - `RES` Research
  - `LOG` Logistics
  - `LYR` War layers
  - `WAR` War orders
  - `EDT` Edit
- Added selected-category action trays while preserving existing prototype behavior.
- Kept factory placement on the existing `ToolType` path; no catalog-ID conversion was attempted in this pass.
- Stopped and deleted the temporary heartbeat once research finished, then decommissioned all research/implementation workers.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-ui-layout-implementation-plan.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-ui-layout-pass-report.md`

Worker reports produced:

- `2026-05-16-twb-trenchworks-ui-reference-research-report.md`
- `2026-05-16-twb-trenchworks-ui-code-audit-report.md`
- `2026-05-16-twb-trenchworks-production-ui-taxonomy-report.md`
- `2026-05-16-twb-trenchworks-local-ui-reference-report.md`

## UI behavior preserved

- Factory/War toggle.
- Factory placement of extractor, belt, assembler, storage, shipping depot, and erase.
- Direction selection.
- Assembler recipe selection.
- War doctrine, entry lane, team spawns, and war layer controls.
- Right tracker tabs, including Research and Logistics shortcuts.
- Pause, speed, and reset buttons.

## Tests/checks run

- Runtime Unity source compile via generated Roslyn response file: passed.
- Editor Unity source compile via generated Roslyn response file with fresh runtime ref: passed.
- Temporary no-window smoke runner: passed.
- Unity Editor log check: latest visible log shows `PrototypeBootstrap.Awake` and first `OnGUI` frame in `TrenchworksPrototype` at `1920x1080`.

Smoke output:

```text
integrated smoke passed=True, ready=True, rp=972, completed=6, teams=2, productionRp=2
prototype ticks=3000, shipments=448, rp=92
```

## Cleanup performed

- Deleted heartbeat: `trenchworks-ui-research-integration-heartbeat`.
- Closed workers: Rawls, Hypatia, Kierkegaard, Carson, and Kuhn.
- Removed temporary compile/smoke directories:
  - `Temp\CodexCompileCheck`
  - `Temp\CodexSmokeCheck`

## Risks

- The bottom rail is now structurally better, but it is still IMGUI prototype UI. It should be reviewed at narrower resolutions before adding more buttons.
- Steam/boiler/pipe buttons are represented conservatively; full catalog-backed placement is deliberately deferred.
- The current visible factory simulation and integrated production facade remain separate. Future UI work should reconcile those before exposing many catalog buildables as placeable objects.
- Category labels are short and functional. Final icons/tooltips will be needed once the build list grows.

## Memory-worthy notes

- The preferred Trenchworks build UI direction is category-first, action-second.
- Use Captain of Industry only as a public UX reference, not as a visual or asset source.
- Strong first-pass category set: Materials, Movement/Transport, Machines, Steam, Assembly, Research, Logistics, Layers, War, Edit.
- Keep research and war detail in the right tracker; the bottom rail should route to those tools rather than duplicate the full UI.

## Follow-up recommendations

- Playtest the new bottom rail in Unity at 1920x1080 and a smaller window size.
- Add hover/status descriptions for category and action buttons.
- Add a proper selected-cell/build inspector on the right panel.
- Later, create a clean mapping between catalog IDs, production facade IDs, and visible factory placement.

## Anything blocked

- No blocker for the UI layout pass. Full catalog-driven building placement is intentionally deferred to a later pass.
