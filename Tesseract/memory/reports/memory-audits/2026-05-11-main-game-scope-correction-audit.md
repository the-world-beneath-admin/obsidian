# Memory Audit Report - 2026-05-11 - Main Game Scope Correction

## Task

Audit the Obsidian memory system after correcting the hierarchy so The World Beneath is treated as the main game and Glassroot Garden is treated as a World Key/subgame.

## Result

The audit found and corrected several scope-drift risks.

The memory system now defaults game-dev, design-decision, marketing, and SEO workflows to The World Beneath main game unless a task brief explicitly scopes the work to Glassroot Garden, another World Key, or shared platform/account systems.

## Files Touched

- `memory/briefs/current-memory-audit-task.md`
- `memory/wiki/game-dev/game-dev-task-workflow.md`
- `memory/wiki/game-dev/systems.md`
- `memory/wiki/game-dev/primary-verbs.md`
- `memory/wiki/game-dev/player-fantasy.md`
- `memory/wiki/game-dev/controls.md`
- `memory/wiki/game-dev/level-design.md`
- `memory/wiki/game-dev/design-constraints.md`
- `memory/wiki/game-dev/technical-constraints.md`
- `memory/wiki/game-dev/enemies.md`
- `memory/wiki/game-dev/open-questions.md`
- `memory/wiki/game-dev/_game-dev-quickref.md`
- `memory/wiki/game-dev/project-hierarchy.md`
- `memory/wiki/game-dev/world-keys.md`
- `memory/wiki/game-dev/core-loop.md`
- `memory/wiki/game-dev/current-mechanics.md`
- `memory/wiki/decisions/design-decisions.md`
- `memory/wiki/decisions/technical-decisions.md`
- `memory/wiki/playtesting/recurring-feedback.md`
- `memory/wiki/playtesting/loved-moments.md`
- `memory/wiki/playtesting/confusion-points.md`
- `memory/wiki/playtesting/next-playtest-questions.md`
- `memory/wiki/competitors/steam-patterns.md`
- `memory/wiki/competitors/seo-patterns.md`

## Checks Run

- Searched memory for stale default-scope language.
- Searched source links for moved Glassroot raw files.
- Verified `memory/raw/game-design/main-game/` now contains only main-game authority/platform docs.
- Verified `memory/raw/game-design/glassroot/` contains Glassroot source docs and the Glassroot handoff.
- Checked largest wiki files for quickref/workflow bloat.

## Corrections Made

- Updated the game-dev workflow so The World Beneath main game is the default scope.
- Added explicit scope language to Glassroot-specific game-dev and playtesting pages.
- Split mixed open questions into main-game questions and Glassroot World Key questions.
- Split mixed competitor/SEO pattern notes into main-game and Glassroot sections.
- Added a Glassroot scope heading to technical decisions.
- Moved Glassroot raw design docs into `memory/raw/game-design/glassroot/`.
- Moved `NEW_WINDOW_HANDOFF.md` out of `memory/raw/game-design/main-game/` because it is a Glassroot handoff, not a main-game authority document.
- Updated wiki source links to point at the new Glassroot raw source folder.

## Risks

- Historical log entries still mention the earlier Glassroot-first seed. That is acceptable because they are chronology, not current authority.
- Raw source files still contain their original wording. That is acceptable because raw evidence should not be rewritten.
- Main-game SEO memory is still a seeded hypothesis layer, not validated keyword-volume or campaign evidence.

## Memory-Worthy Notes

- Decision - Main-game scope is the default unless a task brief says otherwise.
- Warning - Every meaningful task brief must name its scope: main game, Glassroot Garden, another World Key, or shared platform/account system.
- Warning - Raw source folders should stay separated by authority level so subgame docs do not masquerade as parent-game docs.

## Do Not Promote To Memory

- Any judgement about which SEO keyword cluster is strongest. The audit checked organization and scope, not search volume or campaign performance.
- Any claim that Glassroot playtesting feedback exists. The playtesting pages still contain hypotheses only.

## Follow-Up Recommendations

- Create the first scoped pilot task brief for either main-game positioning or main-game Phase 3 priority.
- Run a proper SEO validation pass later with keyword volume, competitor page analysis, and campaign intent notes.
- Keep Glassroot-specific playtesting under World Key scope until main-game playtesting evidence exists.
