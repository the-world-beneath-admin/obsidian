# TWB Trenchworks Worker Report - Tactical Zoom And Minimap

Date: 2026-05-22 10:46
Worker: TWB Trenchworks standing worker
Scope: standalone TWB-tagged game, TWB Trenchworks only

## What Changed

- Raised the war camera minimum cell size from `1.25` to `3.1`, making the current practical tactical view the maximum zoom-out level and removing the absurd whole-map zoom-out from normal play.
- Added an old-school RTS-style minimap overlay at the top-left of the war map viewport.
- The minimap draws:
  - faint transparent black panel and black frame/ring treatment,
  - `Map` label,
  - player and enemy base marks,
  - blue marks for friendly units and integrated war-team members,
  - red marks for enemy units and integrated enemy members only when the player has awareness of the cell,
  - known trench marks,
  - visible/known integrated front blueprint positions,
  - contact pings,
  - current camera viewport box.
- Enemy minimap information is filtered through player awareness using `PlayerVisible`, `PlayerScouted`, or contact age on the corresponding `WarCell`.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-104645-trenchworks-tactical-zoom-minimap.md`

## Checks Run

- `dotnet build "TWB-TrenchWorks.sln" --no-restore`
  - Result: passed with 0 warnings and 0 errors.

## Child Subagent Review

- Child subagent `019e505b-30dd-7b32-92d1-6039a832594f` performed read-only inspection.
- It confirmed:
  - `WarMinCell`, `HandleMapNavigation`, `ClampCamera`, and `EffectiveMinCellSize` are the correct zoom-clamp path.
  - `GetMapRect()` is the right placement basis.
  - The literal top HUD is crowded, so a top-of-war-map overlay is the safer first pass.
  - `WarCell.PlayerVisible`, `PlayerScouted`, `ContactAge`, `WarSubsystemSnapshot.Teams`, `ActiveContacts`, and `VisibleFrontBlueprintPieces` are suitable minimap data sources.
- The child made no edits and ran no tests.

## Cleanup Performed

- Deleted the 2-minute heartbeat automation after implementation.
- Closed the child subagent after reviewing findings.
- No scratch files or generated temporary artifacts were created.

## Risks

- The minimap has not been live-visual-checked in Unity Play Mode in this pass.
- The max zoom-out is set to `3.1` as the screenshot-style tactical zoom floor. Bob may want a slight adjustment after seeing it live.
- Enemy awareness filtering is cell-based. It should be good enough for this prototype slice, but a mature intelligence system may need richer known-unit memory.

## Memory-Worthy Notes

- Bob prefers the screenshot-level tactical zoom as max zoom-out for Trenchworks; whole-map zoom-out makes the play view less useful.
- A minimap is now the intended orientation aid instead of allowing an over-wide camera zoom.
- The minimap should not leak hidden enemy information; enemy marks should stay tied to player visibility, scouting, or contact memory.

## Follow-Up Recommendations

- Live Play Mode review: confirm the minimap does not obscure important battlefield information and that dots are readable at 1080p.
- Add a small click-to-jump interaction later if the minimap becomes a real navigation tool.
- Consider a future HUD layout pass before moving the minimap into the literal top bar.
