# Current TWB Unity Worldmap Task

## Status

Active - updated 2026-05-16 from main-game worker decommission.

## Scope

- Main game / The World Beneath.
- Unity project: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype`.
- Focus: world-map dungeon run reward-loop live verification and narrow polish.

## Worker Role

`twb-main-game-reward-flow-worker`

## Goal

Run a conservative live verification and narrow polish pass after the temporary `DEV COMPLETE` helper and claim rewards modal cleanup. Confirm the world-map dungeon run reward loop works end-to-end before any new gameplay, route/lane, asset, or broad UI work.

Do not perform a broad HoloGlyph UI conversion, route/lane redesign, starter pet expansion, account/persistence pass, asset generation pass, or git cleanup in this milestone.

## Read First

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\slynyrd-pixelblog-reference.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\external-game-dev-resource-index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\main-game-overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\main-game-systems.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-unity\overview.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-unity\world-map-territory-overlay.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-unity\starter-pets-guardian-angels.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-unity\ui-hologlyph-style.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-unity\decisions.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\twb-unity\open-questions.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-icon-wiring-audit-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-unity-run-rewards-dev-complete-report.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-main-game-worker-final-decommission-report.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\UIBoundary\UiWorldMapCommandHandler.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\WorldMapDungeons\WorldDungeonSpawnService.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\UIBoundary\Commands\ClaimWorldMapDungeonRunCommand.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Domain\UIBoundary\WorldMapUiSnapshot.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\Services\WorldMapService.cs`

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TERRITORY_OVERLAY_IMPLEMENTATION_PLAN_2026-05-07.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TERRITORY_SYSTEM_FUTURE_WORK_PLAN_2026-05-07.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\territory_overlay_visual_direction.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\UI_ROADMAP_MASTER_v7.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- unrelated generated creature/enemy/card bulk files unless explicitly assigned
- destructive git operations, broad cleanup, broad staging, or blanket revert/reset operations
- deleting untracked source files without inspection and explicit reason

## Done Criteria

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passes or failures are reported with exact error causes.
- Unity compile/domain reload or editor-status check is run if practical; if open-editor lock blocks batchmode, report it clearly.
- Live editor verifies that a world-map dungeon run can start, the run tracker opens, `DEV COMPLETE` makes the selected run claimable, the claim rewards modal opens, rewards can be claimed, and inventory/node progress update.
- Claim rewards modal is checked for obvious overlap or frame/text collision.
- Any code changes are narrow and directly tied to reward-flow verification.
- A report is written to `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`.

## Report Destination

`C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-twb-main-game-reward-flow-worker-report.md`
