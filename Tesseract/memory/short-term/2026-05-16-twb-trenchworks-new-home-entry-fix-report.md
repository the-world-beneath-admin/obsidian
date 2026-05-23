# 2026-05-16 TWB Trenchworks New Home Entry Fix Report

## Scope

Standalone Unity 2D game under The World Beneath umbrella.

The user declared the new live project home to be:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

The old `prototype` location should no longer be treated as live source.

## What changed

- Treated `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` as the active Unity Hub project.
- Confirmed the new project already contained Trenchworks scripts and `Assets\Scenes\TrenchworksPrototype.unity`.
- Found the remaining problem: Unity's last-opened scene cache still pointed to `Assets\Scenes\SampleScene.unity`.
- Updated `Library\LastSceneManagerSetup.txt` so the project opens `Assets\Scenes\TrenchworksPrototype.unity`.
- Added an editor launch fallback: when Unity opens the project normally, `TrenchworksProjectSetup` now auto-opens `TrenchworksPrototype.unity` if Unity tries to open an empty scene or `SampleScene.unity`.
- Updated the new-home `README.md` so it tells the user to open the new project folder and press Play.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Library\LastSceneManagerSetup.txt`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-new-home-entry-fix-report.md`

Unity also updated normal generated project state while validation ran.

## How to run it in Unity Hub

1. Open this exact folder in Unity Hub:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks
```

2. Let Unity finish compiling/importing.
3. Press Play.
4. Expected result: the Game view shows `TWB Trenchworks Prototype` with running/paused state, tick count, speed, Factory/War Map buttons, factory grid, and war diagnostics.

If Unity somehow opens `SampleScene.unity` again, the editor launch fallback should switch back to `TrenchworksPrototype.unity`. The manual menu remains:

```text
TWB Trenchworks > Open Prototype Scene
```

## Tests/checks run

Entry validation:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks' -batchmode -quit -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.ValidatePrototypeEntryPoint
```

Result: passed. Unity log confirmed the prototype scene opened and the entry point validated.

Simulation smoke test:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks' -batchmode -quit -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest
```

Result: passed.

- first shipment tick: `45`
- first front gain tick: `679`
- final front: `67.5`
- enemy base: `0.0`

Verified after checks:

- `Library\LastSceneManagerSetup.txt` points to `Assets\Scenes\TrenchworksPrototype.unity`.
- `ProjectSettings\EditorBuildSettings.asset` points to `Assets\Scenes\TrenchworksPrototype.unity`.
- Unity/Unity Hub was later observed open on the new project with AssetImportWorker processes; it was left running rather than killed.

## Cleanup performed

- No throwaway scripts or screenshots were created.
- Unity-generated logs/state in the new project were left in place because they belong to the active Unity project import/validation state.
- Permanent Obsidian wiki/index/hot/log memory was not edited.

## Risks

- `Library\LastSceneManagerSetup.txt` is Unity-generated state, so future Unity actions can rewrite it. The editor launch fallback is the more durable guard.
- Batchmode cannot visually confirm the Game view; it confirms compile, scene entry, and simulation behavior. The user should press Play once in Unity Hub for final visual confirmation.
- The old `prototype` path is now obsolete per user instruction and should not be used as live source.

## Memory-worthy notes

- Fact - The live TWB Trenchworks Unity project path is now reported by the user as `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Fact - The new home had Trenchworks assets, but Unity's last-opened scene cache pointed to `SampleScene.unity`.
- Fact - New-home entry validation and simulation smoke checks passed after setting the prototype scene as the launch scene.
- Warning - Treat the old `prototype` path as obsolete unless the user explicitly says otherwise.

## Follow-up recommendations

- User should open the new home in Unity Hub and press Play once.
- If Play visibly works, continue only with small stabilization and diagnostics before adding systems.
- Do not reintroduce nested Unity project folders inside the active project.

## Anything blocked

Nothing blocked.
