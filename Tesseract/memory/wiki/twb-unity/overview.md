# TWB Unity Main Game Lane

## Summary

This lane covers active implementation work in the main **The World Beneath** Unity prototype.

## Project

- Parent project: The World Beneath.
- Local Unity source: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.
- Current implementation focus: HoloGlyph/field-tablet UI conversion, world map territory overlay, node dungeon interaction, and starter pet validation.

## Current State

Recent work converted multiple Unity UI surfaces toward the HoloGlyph/field-tablet visual language and moved world map territory presentation away from heatmap-style spawning toward clustered display-owner nodes, influence fields/rims, routes/lanes, and node-level dungeon interaction.

The world map overlay is functional but not final. Clusters now collapse more properly into town/display-owner summaries, selected WORLD capital pins open compact map-anchored info popups, node dungeon interaction has a first functional movable subwindow, and the full-zoom `z8` pack now also streams from hosted R2 tiles via cache namespace `twb_ops_table_hosted_v20260514`.

The low-zoom world-map pack now has a complete global `z5` overview layer with 1,024 tiles. WORLD capital pins are clickable with compact map popups, and a separate global `z8` land/ocean generation pass is chunking through a reusable ocean fallback catalog.

WORLD capital markers were also corrected away from the muddy detailed scratch pin. The current renderer path uses a dedicated imported/mipped ImageGen display asset with pixel-snapped anchors, but the live visual review is still pending.

Peggy and Stanly starter guardian pets were also stabilized after validation failures. The latest known build after those fixes passed with `0` errors and `4` warnings using:

```powershell
dotnet build TWB_Phase1_IdlePrototype.sln --no-restore
```

The Unity account/persistence lane now has conservative safety slices in source: platform account state is presented as read-only account state rather than an adoptable shared-inventory mirror, and cloud-save loading now uses a two-step confirmation with a local backup before replacing an active local profile. No backend deploys, remote migrations, or production data changes were performed for these slices.

The latest attachment slices now also give Unity a read-only shared companion conflict model, account-state freshness labels, linked inventory adoption into runtime cache only, and a shared pet-icon resolver for starter pet cards plus mirrored monster previews.

That same lane now treats cached account state as a runtime-only projection: the UI can show shared companions, starter selections, exported stacks, and lock/freshness labels, but the main-game inventory remains local-first and cloud-load restore still requires confirmation plus a backup.

Peggy's incorrect `1024` Unity resource has been removed from the project, and the catalog entry now points at the valid `util-peggy` icon for both sprite and key art. The icon audit also says the live material/catalyst/shared skill/modifier/currency sets are already covered, while six special starter skill icons remain the only narrow new art gap.

The long-running main-game worker was decommissioned on 2026-05-16. Durable status from that report:

- generated HoloGlyph material, catalyst, modifier, skill, and currency icon sets are installed as Unity sprites with `.meta` files present
- Inventory V2, Craft Create V2, and Craft Apply V2 have current icon wiring, with live editor click-through still needed
- modifier inventory ids use `card_mod_*`, while generated modifier icon files use `mod_*`; the icon resolver now normalizes this mismatch
- world-map dungeon runs now have a temporary editor/debug-only `DEV COMPLETE` test path for reward-flow verification
- the temporary completion path reuses the existing world-map dungeon claim command/flow rather than granting rewards directly
- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed after the latest reward-flow changes, with 0 errors and 3 warnings
- Unity batchmode compile remained blocked/noisy when another Unity editor instance had the project open; live editor verification is still required

## Current Next Gate

For the main-game reward-flow lane, run a bounded live Unity editor verification pass:

- start a world-map dungeon run
- open the run tracker
- press the temporary `DEV COMPLETE` control
- confirm the claim rewards modal opens without obvious overlap
- claim rewards
- verify inventory and node progress update
- decide whether `DEV COMPLETE` remains editor/debug UI, moves to System Console, or is removed after testing

For the account/persistence lane, continue the read-only shared companion and starter-selection projection slice. Do not write remote inventory, alter backend schema, or let platform stacks overwrite local Will/material/card inventory.

The next design gate is the remote companion mutation protocol: backend event contract, idempotency, lock freshness, conflict resolution, and explicit offline fallback before any write path is enabled.

World-map and starter-guardian visual validation remain separate open gates:

- confirm Unity domain reload/editor state no longer carries stale validation exceptions
- confirm hosted `z8` tiles download, persist, and re-render from cache
- confirm WORLD capital pin popup placement in the live editor

Starter-pet work now has a dedicated lane at [[wiki/twb-unity/starter-pets/overview]].

## Sources

- [[short-term/2026-05-12-twb-unity-worldmap-working-window-intake]]
- [[short-term/2026-05-12-twb-starter-pets-working-window-intake]]
- [[short-term/2026-05-15-twb-unity-icon-wiring-audit-report]]
- [[short-term/2026-05-15-twb-unity-run-rewards-dev-complete-report]]
- [[short-term/2026-05-16-twb-main-game-worker-final-decommission-report]]
- [[wiki/game-dev/project-hierarchy]]
- [[wiki/game-dev/main-game-overview]]
