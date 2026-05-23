# TWB Trenchworks Modern RTS Overlay UI Report

Date: 2026-05-22 11:09

## Scope

Standalone TWB-tagged game: TWB Trenchworks only.

## What Changed

- Changed both factory mode and war mode so the active map draws as the full-screen background.
- Reordered the immediate-mode UI draw pass so the map renders first, then the top bar, right tracker, bottom rail, and command trays render over it.
- Made the top bar, bottom bar, and panels slightly translucent so the game world reads behind the HUD.
- Added map-input blocking for overlay regions:
  - top bar
  - right tracker panel
  - bottom rail
  - bottom tray
  - war minimap panel
- Updated factory placement so clicks on overlay UI no longer place factory entities through the HUD.
- Updated war/factory panning and zoom so scroll/drag over UI overlays no longer moves the map.
- Repositioned the war minimap below the top bar so it behaves like a floating RTS minimap instead of being buried under the HUD.
- Moved map hint text above the bottom tray/rail so it remains readable with the full-screen map.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-22-110912-trenchworks-modern-rts-overlay-ui-report.md`

## Child Subagent

- Child explorer `019e506f-f201-7cc1-bcee-a83987a79cd1` inspected the layout and input risks.
- It confirmed the same safe patch shape: full-screen map rect, draw map first, draw HUD after, block overlay input, and reposition map-owned overlays.
- A 2-minute heartbeat was set during child work and deleted after completion.

## Checks Run

From `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`:

```powershell
dotnet build "TWB-TrenchWorks.sln" --no-restore
```

Result: passed, 0 warnings, 0 errors.

## Cleanup Performed

- Deleted the temporary heartbeat automation after child work completed.
- No scratch files were created.
- No raw GPT Pro package files were modified.
- No staging, commit, reset, or broad cleanup was performed.

## Risks

- Unity Play Mode visual review is still needed to confirm the exact feel at 1920x1080 and smaller windows.
- The right tracker is still a fairly large overlay; it now sits over the world rather than reserving space, but it may need a collapse/minimize button later.
- The factory and war cameras now clamp against the full screen, so the visible composition will shift compared with the old reserved playfield.

## Memory-Worthy Notes

- TWB Trenchworks is moving toward a modern RTS/city-builder presentation model: map as full background, HUD as floating overlays.
- Full-screen map changes must include overlay input blocking, or factory placement and map zoom/pan will leak through UI.

## Follow-Up Recommendations

- Run a Unity Play Mode visual check in both factory and war modes.
- Consider adding a right-panel collapse toggle once the overlay style is visually confirmed.
- Consider making the bottom tray collapse when not actively choosing commands/build tools.
