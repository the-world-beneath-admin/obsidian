# TWB Trenchworks RTS Behaviour Hierarchy Report

## What Changed

- Re-anchored the active task brief to the live Unity project at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Added four read-only research workers for RTS-focused terrain/fog, dig-in, hearing-response, and combat-vision behaviour.
- Made static war-map obstacles readable under fog without treating them as live enemy intelligence.
- Added sustained-contact heat by letting `WarCell.ContactAge` accumulate across repeated fights.
- Allowed non-engineer units to dig low-power foxholes after sustained contact, while engineers/sappers still dig faster.
- Added small contested-vision reveal bubbles around active fights so both fighting units can be seen while contact remains active.
- Added leader-only hearing response: nearby squad leaders move toward active contact from their own side of the fight without magically spotting enemies.

## Files Touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-rts-behaviour-hierarchy-report.md`

## How To Run It

- Open Unity Hub to `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- If the editor is already in Play Mode, stop Play Mode once so Unity can reload scripts.
- Open or keep `Assets\Scenes\TrenchworksPrototype.unity`, then press Play.
- The default wave drill still starts on the war view.

## Prototype My Project Involvement

- `prototype\My project` was not used.
- The obsolete `prototype` folder was not edited or deleted.

## Tests And Checks Run

- Read the live Unity editor log; it showed the current scene bootstrap and first `OnGUI` frame were previously running.
- Attempted Unity batchmode compile. It was blocked because the project is already open in another Unity instance.
- Ran a pure C# source-level compile for non-Unity Trenchworks scripts with Roslyn: passed.
- Ran a Unity-referenced source-level compile including `PrototypeBootstrap.cs` and non-editor scripts: passed.
- Checked for lingering scratch compiler files in `%TEMP%`: none remained.

## Cleanup Performed

- Closed all four research workers.
- Removed temporary compiler response/output files.
- No generated screenshots or throwaway source artifacts were left behind.

## Risks

- Unity batchmode compile could not run while the user’s editor has the project open, so final live Play Mode visual confirmation still belongs in the open editor.
- Static obstacle visibility now reveals battlefield terrain shape earlier; this follows RTS fog convention, but it is a design choice.
- Sustained-contact digging may need tuning if too many foxholes appear or if units hold too early.
- Hearing response is intentionally leader-only to avoid blobs; it may be too subtle until watched at normal speed.

## Memory-Worthy Notes

- RTS fog should separate static terrain knowledge from live enemy movement.
- Active combat should create temporary contested vision, not full enemy-side vision.
- Dig-in behaviour should be contact-heat driven, not only winner/engineer driven.
- Hearing response should move squads toward fight-side support positions without granting omniscient targeting.

## Follow-Up Recommendations

- Live-test at `1x` or `2x` after script reload to see whether sustained contact produces visible foxholes.
- Tune `SustainedContactAge`, `ContactHearingRange`, and reveal radii after one visual pass.
- Later, turn scattered foxholes into trench-network connection behaviour once local contact reads correctly.

## Anything Blocked

- Unity batchmode compile was blocked by the already-open Unity editor instance for `TWB-TrenchWorks`.
- No full visual Play Mode pass was performed from this worker window after the patch.

