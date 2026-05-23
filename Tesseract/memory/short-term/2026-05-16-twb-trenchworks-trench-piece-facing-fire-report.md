# TWB Trenchworks - Trench Pieces, Facing, And Gunfire Report

Date: 2026-05-16
Worker: Bob / TWB Trenchworks playtest stabilization
Scope: Standalone TWB-tagged Unity 2D game, not the main TWB Unity project and not Glassroot Garden.

## What changed

- Added a first prototype trench-piece system: straight, crook, zig-zag, and T-shaped pieces.
- Trench digging now stamps three-tile-wide trench pieces rather than single-cell strips.
- After a faction has a trench network, new trench pieces must connect from an open friendly connector end. Failed random digging now reports that a connector is needed instead of placing an isolated strip.
- Trench cells now remember connector masks and piece kind, allowing connector ends to be consumed/closed when another piece attaches.
- War rendering now draws the actual three-wide trench piece footprint instead of only a one-cell centerline.
- Integrated trench-plan overlays were widened to three tiles so plan hints do not look like old strip trenches.
- Units now track facing direction from movement and combat targeting.
- Unit markers now draw a facing needle.
- Active contacts now draw moving bullet tracers between combat participants.
- The battlefield key now mentions three-wide trench pieces, facing needles, and rifle-fire streaks.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-trench-piece-facing-fire-report.md`

## How to run it in Unity Hub

1. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` in Unity Hub.
2. Open `Assets\Scenes\TrenchworksPrototype.unity` if Unity does not open it automatically.
3. Stop Play Mode if it is already running.
4. Press Play again.
5. Watch for three-wide trench shapes, small connector caps, unit facing needles, and yellow/orange bullet tracers during firefights.

## Whether prototype\My project was involved

No. This pass touched only the live project at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## Tests/checks run

- Watched the live Unity editor log tail after script changes. The current tail shows script reloads and no fresh `error CS`, `Compilation failed`, or `Scripts have compiler errors` markers.
- Ran `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`; it returned success but still warns that the solution contains no projects to restore, so it remains a weak check.
- Source search confirmed the new trench-piece, connector, facing, and tracer hooks are present.

## Cleanup performed

- No scratch files, screenshots, or temporary artifacts were created.

## Risks

- This is a prototype trench-piece rule, not a complete trench-planner. It prevents new random isolated trench placement after a network exists, but it does not yet path units toward connector ends intelligently.
- If a firefight happens far away from existing connector ends, units may fail to dig until movement logic learns to move engineers toward open connectors.
- The three-wide stamp currently uses a simple 3x3 brush along each piece spine. T and crook junctions can be wider at the intersection, which is acceptable for now but may need stricter art masks later.
- Bullet tracers are visual-only and ride on active contact records; they do not yet simulate individual projectile physics.

## Memory-worthy notes

- User wants trenches to be exactly three tiles wide as a rule.
- User wants trench networks to be assembled from premade shapes: straights, T shapes, zig-zags, and crooks.
- After the first trench is laid, new trenches should connect to acceptable connector ends rather than appear randomly.
- Combat readability needs unit facing indicators and visible bullet fire.

## Follow-up recommendations

- Add engineer movement behavior that seeks the nearest open friendly connector before digging.
- Add explicit trench-piece previews/diagnostics in the right panel so we can see connector counts and piece placement failures.
- Replace the temporary 3x3 brush with hand-authored boolean masks per trench piece once the shape library stabilizes.
- Let units inside trenches choose firing bays and face across no-man's-land rather than just facing their current target.

## Blocked

- Full visual acceptance still needs a live Play Mode watch pass after stopping and restarting Play Mode in the editor.
