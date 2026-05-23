# TWB Trenchworks UI Layout Implementation Plan

Date: 2026-05-16
Scope: standalone TWB-tagged Unity 2D game.
Project: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## Research Inputs

- Public reference report: `2026-05-16-twb-trenchworks-ui-reference-research-report.md`
- Code audit report: `2026-05-16-twb-trenchworks-ui-code-audit-report.md`
- Production taxonomy report: `2026-05-16-twb-trenchworks-production-ui-taxonomy-report.md`
- Local reference report: `2026-05-16-twb-trenchworks-local-ui-reference-report.md`

Captain of Industry was used only as a public/user-facing reference for interaction grammar: category recall, dense trackers, readable status, overlays, inspectors, and planning tools. No proprietary code, binaries, or assets were inspected or copied.

## Direction

Replace the current flat bottom rail with a category-first rail:

```text
MAT | MOV | MAC | STM | ASM | RES | LOG | LYR | WAR | EDT
```

The category rail should open compact action trays. It should not expose every future buildable at once, and it should not break the current working `ToolType` placement path.

## First Implementation Slice

### 1. Add Category State

In `PrototypeBootstrap.cs` add:

- `BuildCategory` enum.
- `selectedBuildCategory`.
- helpers for selecting a category.
- small rail status text showing current category and selected action.

### 2. Rework Bottom Rail

Use three areas:

- left: War/Build toggle plus category circles.
- middle: selected-category action circles.
- right: persistent pause/speed/reset.

### 3. Category Action Mapping

Initial actions:

- `MAT`: Extractor, material-oriented recipes if useful.
- `MOV`: Belt plus direction arrows.
- `MAC`: Extractor, Assembler.
- `STM`: open/choose steam layer, show boiler/pipe as locked/future placeholders.
- `ASM`: assembler recipes: ammo, trench materials, rations, medical.
- `RES`: open the Research tracker and show existing Tier 1 research controls there.
- `LOG`: Storage, Shipping Depot, open Logistics tracker.
- `LYR`: Surface, Tunnel, Supply, All.
- `WAR`: doctrine, entry lane, team spawn controls.
- `EDT`: Erase.

Long/future items may appear as locked/placeholder buttons only if they help explain the roadmap. Avoid clutter.

### 4. Preserve Existing Behavior

These must still work:

- place extractor, belt, assembler, storage, shipping depot.
- erase.
- set direction.
- set assembler recipe.
- toggle Factory/War view.
- set doctrine.
- select entry lane.
- spawn available teams.
- switch war layers.
- pause/speed/reset.
- right tracker tabs including Research.

### 5. Do Not Yet

- Do not convert factory placement to full catalog ID placement in this pass.
- Do not debit team spawns from production inventory yet.
- Do not build a full tooltip system yet.
- Do not copy Captain of Industry visual assets or exact category scheme.
- Do not add Tier 4/5 build buttons.

## Implementation Ownership

Because the visible UI is concentrated in `PrototypeBootstrap.cs`, only one code worker should edit the UI source file. Splitting the same IMGUI file across multiple workers would create unnecessary conflicts.

## Verification

- Run runtime source compile via the generated Unity Roslyn response file.
- Run editor source compile via the generated Unity Roslyn response file.
- Run a temporary no-window smoke runner if practical.
- Note whether the already-open Unity Editor log may contain stale errors until Unity refreshes.

## Risks

- Bottom rail can overflow at 1080p if too many actions are visible at once.
- Current factory simulation and integrated production facade are still separate; category actions should not pretend facade-only buildables are visible map objects.
- Research and war should remain tracker-driven; the bottom rail should route to them rather than becoming a giant second UI.
