# 2026-05-16 TWB Trenchworks Dynamic Warfront Rendering Report

## Scope

Standalone Unity 2D TWB Trenchworks prototype under The World Beneath umbrella.

Live project:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

This pass did not touch The World Beneath main Unity game, Glassroot Garden, The Alchemy Lab, TWB-Marketing, shared platform/accounts, pets, sprite-sheet automation, crafting/logistics reports, or permanent Obsidian memory/wiki/index/hot/log files.

## What changed

- Removed the old war-map visual treatment that painted a large moving vertical abstract front:
  - no more solid player-side territory slab from the base to `FrontProgress`,
  - no more no-man's-land/enemy slab split by `FrontProgress`,
  - no more vertical front stripe,
  - no more fake trench band tied to `FrontProgress`.
- Kept the compatibility `FrontProgress` value for smoke tests and compact strategic UI, but relabeled the top tracker from `FRONT` to `PRESSURE`.
- Updated the right-hand war tracker label from `Front progress` to `Pressure summary`.
- Added dynamic map rendering based on actual agent/cell state:
  - base zones,
  - unit influence patches,
  - stronger influence around command/fighting units,
  - trench/foxhole ownership glow,
  - contact glow,
  - existing obstacles,
  - existing units,
  - existing contact markers.
- Removed the old center-map command/enemy icons that were positioned by `FrontProgress`.
- Updated the map hint to explain that control is coming from units, trenches, contacts, and bases.
- Updated the README to say the war map no longer draws a solid moving abstract front band.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\README.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-dynamic-warfront-rendering-report.md`

## Tests/checks run

- Source check confirmed the old `frontX`, `trenchBand`, `playerBaseEnd`, and `enemyBaseStart` war-rendering paths were removed from `PrototypeBootstrap.cs`.
- Unity Roslyn compile check for `Assembly-CSharp` passed with exit code `0`.
- Attempted Unity batch smoke test, but Unity refused to open a second copy of the project because the user's editor already had it open.

Exact blocker:

```text
Aborting batchmode due to fatal error:
It looks like another Unity instance is running with this project open.

Multiple Unity instances cannot open the same project.

Project: C:/Users/yrred/Desktop/Unity/TWB-Trenchworks/TWB-TrenchWorks
```

## Cleanup performed

- Removed temporary compile/smoke output folder:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Temp\CodexCompileCheck
```

## Risks/open questions

- The top pressure bar still uses the existing compatibility `FrontProgress` value. It is no longer drawn as a map stripe, but the value itself still partly comes from the legacy strategic smoke path.
- Dynamic influence patches are visual-only and derived from live units/trenches/contacts. They are not yet persistent cell-control data.
- The war map should now look less abstract, but live visual review in the open Unity editor is still needed.
- Because Unity was open, the full batch smoke test could not run in this pass.

## Follow-up recommendations

- Press Play in the already-open Unity editor and confirm the war map shows local patches, units, trenches, obstacles, contacts, and bases instead of a moving vertical stripe.
- Next, add explicit cell-control values or sector summaries derived from unit proximity, trench ownership, and recent contacts.
- Later, make `FrontProgress` itself fully derive from the agent/cell model and rename the compatibility field when smoke tests are updated.
- Add hover/click inspection so a player can inspect why a patch is friendly, enemy, contested, or neutral.

## Anything blocked

Only the Unity batch smoke test was blocked by the already-open Unity editor instance. Roslyn compile passed.
