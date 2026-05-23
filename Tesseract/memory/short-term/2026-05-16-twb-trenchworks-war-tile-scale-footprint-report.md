# TWB Trenchworks War Tile Scale And Unit Footprint Report

Date: 2026-05-16
Worker: Bob / Trenchworks playtest stabilization
Scope: TWB Trenchworks standalone Unity 2D prototype

## What Changed

- Set war map maximum zoom to 64 pixels per tile.
- Set ordinary war-unit visual markers to occupy a 2x2 tile art footprint at max zoom.
- Set command/lieutenant war-unit visual markers to occupy a 2x4 tile art footprint at max zoom.
- Kept this as a visual/art-scale contract only. Simulation collision, pathing, and occupancy were not broadened into 2x2 or 2x4 physical blockers.
- Preserved full visual unit footprint while entrenched instead of shrinking the marker down to a small strip.
- Scaled facing indicators so they remain readable on the larger unit footprints.
- Fixed a compile-blocking trench-piece switch expression by parenthesizing the modulus expression.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-tile-scale-footprint-report.md`

## How To Run It In Unity Hub

Open the canonical Unity project:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

Open or confirm the scene:

`Assets\Scenes\TrenchworksPrototype.unity`

Press Play. The war view can zoom in to 64 pixels per tile. At that maximum zoom, ordinary soldiers are drawn as 2 tiles wide by 2 tiles tall, and command/lieutenant units are drawn as 2 tiles wide by 4 tiles tall.

## Whether `prototype\My project` Was Involved

No. This pass used only the new canonical project home:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

The old nested `prototype\My project` path was not touched.

## Tests And Checks Run

- Searched the Unity render/bootstrap code for war zoom and unit marker hooks.
- Confirmed source hooks for `WarMaxCell`, unit visual tile constants, and trench marker behavior with `rg`.
- Ran `dotnet build` on `TWB-TrenchWorks.sln`; it reported success but warned that the solution has no project to restore, so this is only a weak check.
- Checked the Unity editor log. It still contained the previous trench-piece compile error from before the fix.
- Ran Unity's Roslyn compile command directly against the updated `Assembly-CSharp` response files; it completed with exit code 0 and no compiler output.

## Cleanup Performed

- No scratch files, screenshots, or throwaway logs were created for this pass.
- No project folders were deleted.

## Risks

- The 2x2 and 2x4 sizes are currently visual footprints only. Actual gameplay occupancy is still based on the existing unit position logic.
- Unit culling still keys off the unit anchor/logical cell, so very large future sprites may need expanded viewport culling near screen edges.
- At 64 pixels per tile, the player sees far fewer tiles at maximum zoom. This is good for sprite readability, but the tactical overview depends more heavily on zooming back out and squad aggregation.
- The open Unity Editor may need Play stopped/restarted or the editor refocused so it reloads the latest source after its previous compile failure.

## Memory-Worthy Notes

- Trenchworks war-map art scale is now anchored to a Factorio-like high-resolution tile standard: 64 pixels per grid tile at maximum zoom.
- Base soldiers are intended as 2x2 tile art units.
- Command/lieutenant units are intended as 2-wide by 4-tall tile art units.
- This should guide future sprite mockups and unit visual hierarchy, but should not automatically imply larger physical pathing footprints.

## Follow-Up Recommendations

- After the user confirms the scale feels right in Play mode, add dedicated placeholder sprites or stronger silhouette boxes for 2x2 soldiers and 2x4 lieutenants.
- Decide separately whether large command units should have larger collision/occupancy, or remain large visual markers over a compact command position.
- Add a small in-game zoom readout that explicitly says `64 px/tile` at maximum zoom for art-scale testing.
- Revisit unit labels after sprite placeholders exist; current labels may be too small relative to the new art footprint.

## Anything Blocked

- No source-level blocker remains from this pass.
- Full live Unity verification depends on the already-open editor reimporting the changed scripts and entering Play cleanly.
