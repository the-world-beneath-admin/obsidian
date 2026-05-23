# TWB Unity Decisions

## Active Decisions

- Decision - Main Unity world map territory display should collapse raw anchors into display-owner/town summaries.
- Decision - Folded child anchors should become owner badges/intensity rather than independent map clutter.
- Decision - Territory connections should attach to display owners, not raw/folded child anchors.
- Decision - Node dungeon interaction should open a movable subwindow summarizing dungeons at the clicked node.
- Decision - Peggy is a Faith utility starter.
- Decision - Stanly is a Might attack starter.
- Decision - Starter guardians should be high-end Tier 1 Legendary creatures, not over-tier stat outliers.
- Decision - Do not add `special_ephemrial_spirit` to the global biome registry just to satisfy starter pets.
- Decision - Do not weaken tier/stat/skill validators to make Peggy or Stanly pass.
- Decision - Special protected starter creatures may skip regular biome/family slice validation, but still must pass creature envelope, tier, and skill affinity contracts.
- Decision - Starter pets do not receive monster/enemy mirror versions.
- Decision - Starter pet special identity/display lane can be `Ephemrial Spirit`, but combat mechanics still require normal A-Series affinities such as Faith or Might.
- Decision - Starter selection UI remains deferred until explicitly assigned.
- Decision - Main Unity should treat platform account/inventory state as read-only display data until an explicit import/export contract is approved.
- Decision - Loading a cloud save over an active local profile should use an explicit confirmation step and create a local backup first.
- Decision - Shared companion assignment prep should use a central read-only `SharedCompanionAssignmentConflictModel`; local invalid/wrong-role/local-activity locks block first, cached account locks block next, missing projection is warning-only, and account-ready companions still flow through local/offline assignment.
- Decision - Pet card icons and mirrored monster previews should reuse the imported pet-icon pipeline until dedicated monster art is needed.
- Decision - The world-map dungeon run `DEV COMPLETE` path is temporary editor/debug test support only, not player-facing gameplay.
- Decision - The temporary dungeon run completion path should reuse the existing world-map dungeon claim flow rather than directly granting rewards.
- Decision - HoloGlyph modifier icon resolution must normalize `card_mod_*` inventory ids to generated `mod_*` icon ids.

## Warnings

- Warning - The Unity worktree may be heavily dirty with unrelated or generated changes. Do not blindly revert, reset, stage, or commit everything.
- Warning - Some untracked files may be important to compile/runtime behavior; inspect before cleanup or commit.
- Warning - `ephemrial` is misspelled in ids/file names; do not rename it casually without migration.
- Warning - Starter pet special affinity and combat A-Series affinity are separate concepts.
- Warning - Do not use `AffinityId.Unknown` for starter pet skills, creatures, cards, or metadata.
- Warning - The latest regenerated Stanly sprite still needs user acceptance before it is treated as final.
- Warning - Unity generated solution files may not see newly-created C# files until Unity refresh/regeneration; if immediate `dotnet build` validation is needed, inspect project inclusion before assuming a code error.
- Warning - Unity automation status may report failure/noise when another editor has the project open or shutdown lines are parsed; check the Unity/editor logs before treating it as a product compile failure.
- Warning - The temporary `DEV COMPLETE` helper should be removed, moved to System Console, or kept editor/debug-only before release-facing builds.

## Sources

- [[short-term/2026-05-12-twb-unity-worldmap-working-window-intake]]
- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-15-twb-unity-icon-wiring-audit-report]]
- [[short-term/2026-05-15-twb-unity-run-rewards-dev-complete-report]]
- [[short-term/2026-05-16-twb-main-game-worker-final-decommission-report]]
