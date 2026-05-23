# TWB Trenchworks War Team Authority Field Map Pass Report

## Scope

Standalone TWB-tagged Unity 2D game: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This pass responds to the GPT Pro recommendation to stop relying on independent local soldier movement and begin moving the live visible battlefield toward team authority plus shared battlefield field maps.

## What Changed

- Added `WarSquadIntent` to the visible `WarWorld` layer: `Scout`, `SupportContact`, `FormFiringLine`, `Hold`, `DigIn`, `Retreat`, and `Regroup`.
- Added per-unit squad debug fields: shared squad intent, shared squad reason, shared squad target, suppression, confidence, combat edge, and squad order age.
- Added `UpdateSquadOrders()` so command/squad-leader units choose a squad intent before individual soldiers execute movement.
- Added cheap shared field-map sampling inside the live visible war simulation:
  - cover
  - contact heat
  - danger
  - friendly support
  - supply reach
  - trench safety
  - blob penalty
  - no-man pressure
- Changed followers so they stay in tighter leader formations instead of resuming independent scouting when not directly fighting.
- Made contact outcomes broadcast squad-level dig-in or retreat intent when one side gets a clear edge.
- Added suppression and confidence updates from fire, cover, trench safety, contact heat, and danger.
- Exposed squad intent, suppression, confidence, and combat edge in the right-hand unit summary and selected-unit text.
- Replaced the remaining trench-piece `% switch` expression with classic `switch` statements so Unity's editor compiler does not choke on that syntax edge.
- Refreshed the active Trenchworks task brief from the old trench-pattern pass to the new war team authority/field-map bridge pass.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-war-team-authority-field-map-pass-report.md`

## How To Run It In Unity Hub

1. Open Unity Hub to `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
2. Open `Assets\Scenes\TrenchworksPrototype.unity`.
3. Press Play.
4. The war wave drill should start on the war screen. Select/click units or use the right-hand Unit Summary.
5. Look for command rows showing intent plus `S` suppression and `C` confidence, and selected-unit text showing intent, edge, and suppression.

## Whether `prototype\My project` Was Involved

No. This pass only touched the live canonical project at:

`C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

The obsolete nested sample project was not used or modified.

## Tests / Checks Run

- Direct Unity Roslyn compile from the live project passed with no output:

```powershell
& "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\NetCoreRuntime\dotnet.exe" exec "C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Data\DotNetSdkRoslyn\csc.dll" /nostdlib /noconfig /shared "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp" "@Library\Bee\artifacts\1900b0aE.dag\Assembly-CSharp.rsp2"
```

- `dotnet build TWB-TrenchWorks.sln` passed, with the known weak Unity solution warning: `Unable to find a project to restore`.
- Live editor log showed an old compile error against the trench-piece `% switch` syntax. The source was changed to classic `switch` statements afterward, and direct Unity Roslyn compile passed again.
- Unity batch smoke was not launched because the Unity editor is already open on this project.

## Cleanup Performed

- No temporary files, screenshots, or scratch artifacts were created.
- No obsolete prototype folder cleanup was performed.

## Risks

- This is a bridge in `WarWorld`, not the full final cutover where `WarTeamSlice` owns the visible battlefield. The two-brain architecture still exists, but the visible layer now has squad-level intent and field-map scoring.
- The field-map sampling is intentionally cheap and local. It should be good enough to test behavior, but it is not the final low-resolution cached influence-map system.
- Live Play Mode behavior still needs visual review after Unity refreshes/recompiles in the open editor.
- Tuning may swing between overcautious squads and overly aggressive squads until the contact-to-dig loop is visually verified.

## Memory-Worthy Notes

- GPT Pro's recommendation is accepted as the next war milestone direction: `War Team Authority And Frontline Field Maps`.
- The correct next proof is not more units or UI polish. It is: scout, find contact, form firing line, gain edge, dig in, hold, connect trenches, and keep supply relevant.
- Visible debugging must remain part of the system. Unit rows now expose intent, suppression, confidence, and combat edge so AI behavior can be judged without guessing.

## Follow-Up Recommendations

- Run a live Play Mode review and watch whether command units now show `Scout`, `SupportContact`, `FormFiringLine`, `DigIn`, `Hold`, `Retreat`, or `Regroup` as the fight evolves.
- If squads still stall, add an explicit order-timeout/probe rule at the squad level rather than individual jitter.
- Next code pass should connect trench network IDs and supply connection state to squad intent.
- Later, replace the cheap per-sample field-map functions with cached low-resolution influence maps updated at slower intervals.

## Anything Blocked

- Full Unity Play Mode verification is still blocked from this worker because the editor is open interactively. The source-level compile passed; the user/Bob should verify the live scene visually after Unity recompiles.
