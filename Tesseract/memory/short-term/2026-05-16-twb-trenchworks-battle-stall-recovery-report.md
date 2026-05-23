# TWB Trenchworks Battle Stall Recovery Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D prototype.

## User Signal

The live wave drill appeared to stall: many units were alive, many were in `Holding`, active contacts dropped to zero, and the fight stopped advancing.

## Diagnosis

Completed trenches were acting as absolute stop signs. `TickUnit()` checked weapon range, then `TryHoldCompletedFriendlyTrench()` returned immediately for any unit on a completed friendly trench. Once both sides settled into trenches outside weapon range, no one created new contact. Because the wave drill has an alive-unit cap, it could then fill up with living units that were all politely holding ground.

## What Changed

- Added quiet-front tracking when the wave drill has no active contacts.
- After the front is quiet for 10 strategic seconds, some squad leaders begin probing forward from completed trenches.
- Followers can leave completed trenches to catch up with a probing commander.
- Enemy squad leaders in held trenches can be reactivated during quiet-front recovery so the other side can also probe instead of remaining static.
- Completed trenches still hold normally while contact exists or while the quiet-front delay has not elapsed.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-battle-stall-recovery-report.md`

## Tests And Checks

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Passed, though Unity's generated solution still reports no standard project to restore.
- Unity editor log tail checked after the change.
  - No current `CS` compiler errors were found in the checked tail.

## Cleanup Performed

- No temporary files, screenshots, or scratch artifacts were created.

## Risks

- The probe cadence is intentionally conservative. If the battle still goes quiet too long, reduce the quiet-front delay or increase the percentage of leaders selected to probe.
- This keeps dug-in defense, but it does let leaders rotate forward once the whole battlefield is quiet. That is a gameplay compromise to keep the simulation alive.
- It does not yet add a proper order system for reserve/assault teams. This is a tactical stall recovery, not the final command doctrine model.

## Memory-Worthy Notes

- Permanent hold states need a recovery path when the global front is quiet.
- The trench rule should be: units defend established positions during/near contact, but squad leadership can restart scouting/probing when the front goes inactive.
- Current wave-drill alive caps make stall recovery more important because no new squads spawn once both sides are capped.

## Follow-Up Recommendations

- Live test until contacts hit zero, then watch for log line: `Front went quiet; squad leaders begin probing out from held trenches.`
- If still too static, expose quiet-front seconds and probing leader counts in the right panel.
- Later, replace this with explicit squad orders: hold trench, probe, assault, resupply, rotate/recycle.

## Blocked

- No live Play Mode verification was performed in this pass.
