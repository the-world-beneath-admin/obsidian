# TWB Trenchworks Decommission Intake

Date: 2026-05-19
Source report: [[short-term/2026-05-19-twb-trenchworks-worker-final-decommission-report]]

## Reviewed

Bob/orchestrator reviewed the Trenchworks final decommission report and promoted durable implementation state, warnings, and the next gate.

## Promoted

- Trenchworks Phase 1 front generation has advanced from planning into a staged front-generation implementation.
- Current reported generator features: two actual front lines, clean no-man's-land except intended protrusions, access trenches, support lines, supply/spawn-link branches, empty hardpoint pads, front-line MG sockets, and additive F9 diagnostics.
- Front-line MG points are now an empty-socket contract tied to Wave 1 front trench cells, not rear/support hardpoints and not pre-manned nests.
- Old explicit `CMD`/`MTR` Phase 1 anchors were confirmed as `CommandDugout` and `MortarPit` paths and removed from initial generation.
- Command/mortar functionality should return later through empty hardpoint pads and specialist claim/build flows.
- Soldier V2 sprites are the major war-side asset class to keep; older non-soldier war art is mostly legacy/reference until runtime callers and replacements are mapped.
- Passing `dotnet build` remains insufficient for the current gate; Unity import/Play Mode/F9 visual verification is required.
- Next gate is live Unity/F9 visual verification. If it passes, commission `Phase 1 Front Blueprint Sprite Pack v4`.

## Updated Memory

- [[wiki/twb-trenchworks/overview]]
- [[wiki/twb-trenchworks/architecture]]
- [[wiki/twb-trenchworks/open-questions]]
- [[briefs/current-twb-trenchworks-task]]
- [[hot]]
- [[index]]
- [[log]]

## Not Promoted

- Exact child-worker chatter and subagent sequencing.
- Unverified claim that all hardpoint visuals are final.
- Old manned MG/mortar/command art as final runtime assets.
- Asset counts as permanent production truth.
- Older `24` unit-count docs; this remains an open reconciliation question against newer reported `33` war member roles.

## Next Gate

Start a fresh Trenchworks worker. It should run live Unity/F9 visual verification first, then either report the staged generator as visually acceptable or make the narrowest generator/F9 correction before asset production.
