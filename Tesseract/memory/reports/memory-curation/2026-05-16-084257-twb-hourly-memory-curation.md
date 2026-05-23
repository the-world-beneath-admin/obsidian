# 2026-05-16 08:42:57 - TWB Hourly Memory Curation

## Lock Status

- Acquired cleanly with exclusive create semantics at the start of the run.
- No stale lock recovery was needed.

## Reports Reviewed

- `memory/short-term/2026-05-16-twb-trenchworks-playtest-stabilization-report.md`
- `memory/short-term/2026-05-16-twb-trenchworks-map-props-implementation-report.md`
- `memory/short-term/2026-05-16-twb-trenchworks-fog-readability-reveal-report.md`
- `memory/short-term/2026-05-16-twb-trenchworks-squad-leader-ai-tree-research.md`
- `memory/short-term/2026-05-16-twb-trenchworks-squad-leader-ai-implementation-plan.md`
- `memory/short-term/2026-05-16-twb-trenchworks-squad-leader-ai-implementation-report.md`
- `memory/short-term/2026-05-16-glassroot-garden-plot-selection-sparkle-report.md`
- `memory/short-term/2026-05-16-glassroot-garden-worker-break-portal-door-layered-animation-report.md`
- `memory/short-term/2026-05-16-twb-creature-spritesheet-auto-mi-13.md`
- `memory/short-term/2026-05-16-twb-creature-spritesheet-auto-mn-01.md`

## Items Promoted

- Trenchworks now has a more specific squad-leader memory note: `WarTeamSlice` uses a shared blackboard, utility-style candidate scoring, combat-edge bias toward hold/dig-in, lateral movement, and formation collision avoidance. This is the durable part of the latest AI pass.
- The Garden now has a durable sparkle interaction note: empty selectable plots emit a runtime sparkle field on hover and while the seed bag is waiting for a packet choice, then clear once a packet is selected.
- The Garden current focus was tightened to include plot-selection sparkle behavior alongside the existing worker-break door timing and selector alignment gate.

## Items Kept Only In Reports

- Exact Trenchworks smoke outputs, map dimensions, and playtest counters from the stabilization and fog/readability reports.
- Trenchworks implementation details that are already well represented in the wiki, including the broad war-map prop set and the general shared-leader AI direction.
- Garden screenshot filenames, browser probe minutiae, and the detailed portal/door timing sequence beyond the durable layer separation already captured in memory.
- Sprite-sheet provenance, raw filenames, finishing-pass counts, and temporary scratch cleanup notes from `MI-13` and `MN-01`.

## Items Rejected Or Ignored

- Did not promote the direct-repack-vs-chroma-helper preference as a permanent rule yet; it is useful but still too narrow and report-specific.
- Did not duplicate the `MI-13` and `MN-01` completion state in permanent memory because the sprite lane already holds that queue state.
- Did not promote transient browser timing, screenshot paths, or raw QA counts.

## Files Changed

- `memory/hot.md`
- `memory/index.md`
- `memory/wiki/twb-trenchworks/overview.md`
- `memory/wiki/twb-trenchworks/architecture.md`
- `memory/wiki/world-keys/the-garden/overview.md`
- `memory/wiki/world-keys/the-garden/testing.md`
- `memory/reports/memory-curation/2026-05-16-084257-twb-hourly-memory-curation.md`

## Open Questions / Conflicts

- The Garden still has the separate user-visible plot plant/bar artifact question open in clean Playwright versus local browser state.
- Trenchworks still needs the next visible Unity Play Mode smoke after the editor refreshes scripts, even though the source-side AI and simulation checks passed.

## Next Recommended Gate

- Run the live Garden browser review at `http://127.0.0.1:5173/` and confirm worker-break door scale/timing, selector alignment, plot-selection sparkle behavior, compost/sign layout, plot outline clarity, and slower companion movement.
- Then refresh the Trenchworks Unity editor and do the visible Play Mode smoke to confirm the smarter squad layer is reflected in the live battlefield view.
