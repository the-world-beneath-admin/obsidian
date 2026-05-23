# TWB Trenchworks Cover And Grenade Combat Pass Report

Date: 2026-05-16

## Scope

Standalone TWB-tagged game: TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## What Changed

- Added a small full-cover casualty leak so full cover and deep trenches greatly reduce danger but no longer create perfect immunity.
- Added grenade attacks as a local anti-stalemate rule:
  - Grenades can be thrown at short range.
  - They cost ammo.
  - They are more likely from sappers, engineers, and riflemen.
  - They mainly trigger against strong cover, trenches, suppression, or sustained contact.
  - They bypass some cover, add suppression, and can splash a couple of nearby squadmates.
- Added grenade-specific contact summaries and battle-log notes so the reason for sudden cover casualties is visible.
- Added grenade visual cues in the war view: blast square/ring plus a simple arcing contact line instead of ordinary rifle tracers.
- Added null guards to the war map and Unit Summary UI so Unity domain reloads do not briefly repaint before `simulation.War` is ready.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-cover-grenade-combat-pass-report.md`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open or confirm scene `Assets\Scenes\TrenchworksPrototype.unity`.
4. Press Play.
5. Watch covered firefights after trenches form. Full cover should still protect heavily, but prolonged covered fights should now sometimes produce casualties, grenade bursts, suppression, or forced movement.

## Whether `prototype\My project` Was Involved

No. This pass only touched the current live project home: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## Tests And Checks Run

- Read project memory context: `memory/hot.md`, `memory/index.md`, and `memory/wiki/game-dev/project-hierarchy.md`.
- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Result: passed with the existing warning that there is no project to restore.
- Unity response-file compiler:
  - `dotnet exec ... csc.dll ... Assembly-CSharp.rsp ... Assembly-CSharp.rsp2`
  - Result: passed with exit code 0.
- Unity editor log check:
  - Latest editor reload imported scripts, ran `PrototypeBootstrap.Awake`, and rendered first `OnGUI`.
  - An earlier null-reference during Unity repaint was found and guarded; the latest tail did not show it repeating.

## Cleanup Performed

- No temporary files, screenshots, or batchmode logs were created.

## Risks

- Grenade tuning is first-pass. It may be too subtle if stalemates persist, or too lethal if short-range fights collapse too quickly.
- Grenades currently use ammo as a stand-in for a future dedicated grenade/resource chain.
- The full-cover leak is intentionally small but could need adjustment after watching a longer battle.
- Full Unity batchmode smoke was not run because Unity is already open on the project.

## Memory-Worthy Notes

- Full cover should be strong cover, not perfect safety. Trenchworks needs rare attrition through cover plus indirect tools to prevent permanent covered standoffs.
- Grenades are a good early anti-stalemate mechanic for short-range covered fights before adding heavier artillery, mortars, or detailed squad equipment.
- Combat reasons and visuals must expose why casualties happen, especially when units appear protected.

## Follow-Up Recommendations

- Live Play review should watch for whether grenade bursts visibly break covered stalemates without making trenches pointless.
- If stalemates continue, the next breaker should likely be mortar pressure against high-contact trench clusters.
- Later production design should split grenades from generic ammo and make them a supply item.

## Anything Blocked

- No source-level blocker. Live combat feel remains the important verification step.
