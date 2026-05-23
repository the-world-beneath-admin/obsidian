# TWB Trenchworks - Trench Readability And Depth Report

Date: 2026-05-16
Worker: Bob / TWB Trenchworks playtest stabilization
Scope: Standalone TWB-tagged Unity 2D game, not the main TWB Unity project and not Glassroot Garden.

## What changed

- Replaced the visually blob-like trench fill with a narrow trench-network renderer that draws center-line segments, elbows, T junctions, and junction nodes.
- Added stronger trench contrast with a dark cut/shadow, earth rim, and distinct shallow/deep trench core colors.
- Added an on-map key explaining shallow trench, deep trench, and the smaller marker used when a soldier is inside a trench.
- Reduced trench-unit influence patches so units holding trenches do not visually create large control blobs.
- Made soldiers standing in friendly trenches render smaller and darker, with an oriented trench slot beneath them so they read as partially or fully underground.
- Strengthened trench protection in the combat model: shallow trenches now reduce bullet damage more clearly, and developed trenches act closer to full underground cover.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-trench-readability-depth-report.md`

## How to run it in Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. Open `Assets\Scenes\TrenchworksPrototype.unity` if Unity does not open it automatically.
3. Press Play.
4. Use the war view and watch for narrow brown/black trench lines. The battlefield key in the map corner explains shallow trench, deep trench, and units inside trenches.

If Unity was already in Play Mode while these files changed, stop Play Mode once and press Play again so Unity reloads the scripts cleanly.

## Whether prototype\My project was involved

No. This pass touched only the live project at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## Tests/checks run

- Checked the live Unity editor process and log for the active `TWB-TrenchWorks - TrenchworksPrototype` editor window.
- Unity editor log tail after script refresh showed no current `error CS`, `Compilation failed`, or `Scripts have compiler errors` markers.
- Ran `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`; it returned success but warned that the solution contains no projects to restore, so this is only a weak source-level check.

## Cleanup performed

- No scratch files, screenshots, or temporary artifacts were created.

## Risks

- This pass fixes trench readability and unit-in-trench presentation. It does not yet fully constrain the underlying digging simulation to enforce a hard 2-3 tile trench-width rule.
- If many units dig adjacent cells at once, the renderer will hide much of the blob effect, but a later simulation pass should make squads plan trench lines rather than independently carpet-digging.
- The battlefield key occupies a small overlay area in the map corner; it may need repositioning if it hides important action at certain zoom levels.

## Memory-worthy notes

- User wants trenches to read as narrow line networks with T junctions and zigzags, not large filled blobs.
- Developed trenches should mean soldiers are functionally underground/full-cover; shallow trenches should mean partial cover.
- Soldiers inside trenches should visually sit into the trench and fight from that position.

## Follow-up recommendations

- Add a trench-planning pass that makes engineers extend trench heads, build zigzag/fire bays, and avoid dense carpet digging.
- Give trench cells explicit visual states: foxhole, shallow trench, developed trench, communication trench.
- Add unit behavior that prefers entering nearby friendly trenches during fights instead of standing adjacent to them.
- Add a small trench-network diagnostic to count dense blocks and catch future blob regressions.

## Blocked

- Full Play Mode visual confirmation still needs the user to stop and restart Play in the open Unity editor, then watch a wave drill long enough for contact and trench development.
