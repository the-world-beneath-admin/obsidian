# TWB Trenchworks Research Intake

## Status

Complete - 2026-05-15.

## Source Reviewed

- [[short-term/2026-05-15-twb-trenchworks-research-plan]]

## Promoted

- TWB Trenchworks remains a standalone Unity 2D project under the TWB umbrella, not a browser game.
- Phase 1 is player-versus-NPC.
- The player supplies one faction in phase 1.
- Multiplayer is desired later but not in phase 1.
- Shared account systems and shared pet systems are not in phase 1.
- War outcomes should target roughly 80 percent supply-driven and 20 percent seeded random variance.
- Player unit choice should be requisition/spawn strategy, not direct tactical control.
- Command units are promising as autonomous leaders that assemble non-command units into mission teams.
- Recommended technical direction is pure C# simulation plus Unity presentation.
- Recommended rendering direction is hybrid Tilemap/custom grid.
- First prototype should prove that factory output changes war outcomes.

## Kept Report-Only

- Specific placeholder recipes and resource names.
- Suggested map/grid sizes.
- Suggested class/module names.
- Exact provisional unit roster.
- Full Factorio and Unity research synthesis.
- Jokes and wording from the worker report, charming though they may be.

## Files Changed

- `memory/wiki/twb-trenchworks/overview.md`
- `memory/wiki/twb-trenchworks/open-questions.md`
- `memory/wiki/twb-trenchworks/research-plan.md`
- `memory/wiki/twb-trenchworks/architecture.md`
- `memory/briefs/current-twb-trenchworks-task.md`
- `memory/index.md`
- `memory/hot.md`
- `memory/log.md`

## Remaining Blocked

Implementation is blocked until the user answers the implementation-shaping design questions:

- tone
- victory condition
- session shape
- command-control level
- phase-one unit roster
- war view style
- resource naming style

## Next Gate

Ask the user for the design choices above, then create a narrow Unity prototype brief. Do not start implementation until that brief exists.
