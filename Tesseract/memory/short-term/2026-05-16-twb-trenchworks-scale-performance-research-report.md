# TWB Trenchworks Scale Performance Research Report

Date: 2026-05-16
Scope: TWB Trenchworks standalone Unity 2D prototype.

## User Signal

The wave drill still slows down badly after the first soldier waves. The immediate need is smoother large-scale war simulation before adding more systems.

## Research Sources

- Unity profiling guidance: https://unity.com/how-to/best-practices-for-profiling-game-performance
- Unity application profiling manual: https://docs.unity.cn/Manual/profiler-profiling-applications.html
- Unity ProfilerMarker guide: https://docs.unity.cn/Packages/com.unity.profiling.core%401.0/manual/profilermarker-guide.html
- Unity ProfilerRecorder API: https://docs.unity.cn/6000.2/Documentation/ScriptReference/Unity.Profiling.ProfilerRecorder.html
- Unity garbage collection best practices: https://docs.unity.cn/Manual/performance-garbage-collection-best-practices.html
- Unity OnGUI API: https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.OnGUI.html
- Unity EventType.Repaint API: https://docs.unity.cn/2018.1/Documentation/ScriptReference/EventType.Repaint.html
- Unity job system overview: https://docs.unity.cn/Manual/JobSystem.html

## What Changed

- Removed a duplicate fog simulation activation pass inside the war strategic tick.
- Added Unity Profiler markers for:
  - `TWB.Trenchworks.SimulationTick`
  - `TWB.Trenchworks.FactoryMapDraw`
  - `TWB.Trenchworks.WarMapDraw`
  - `TWB.Trenchworks.WarUnitSummaryDraw`
- Limited heavy custom map drawing to IMGUI repaint events after input/navigation has been handled.
- Converted far-zoom scouted/fog ground drawing into coarse blocks instead of thousands of tiny per-cell `GUI.DrawTexture` calls.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-twb-trenchworks-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-scale-performance-research-report.md`

## Checks Run

- `dotnet build C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\TWB-TrenchWorks.sln`
  - Passed, but the generated Unity solution has no standard .NET project to restore, so this is only a weak source-level check.
- Read the live Unity editor log after script import.
  - Unity compiled changed scripts and reloaded assemblies with no `CS` compiler errors shown.
  - Unity is already open, so I did not run a separate batchmode Unity process against the same project.

## Diagnosis

The slowdown is probably mixed CPU/UI rather than a single villain:

- IMGUI `OnGUI` can run multiple times per frame, so map drawing work was being repeated on non-render events.
- The war map was using many small `GUI.DrawTexture` calls for remembered/scouted ground as fog coverage grew.
- The war tick still has repeated all-unit scans:
  - enemy range checks scan all units;
  - support and engineering checks scan all units;
  - player influence checks scan player units for enemy units;
  - squad grouping and unit summary UI still use LINQ/list allocation patterns.
- Fog visibility reveal touches many cells around every active unit. That is manageable at small counts, but it compounds with 5x speed and many live squads.
- Current active/static fog simulation helps, but it does not yet use proper spatial buckets or cached query results.

## Recommended Optimization Plan

1. Profile with the new markers in Unity Profiler.
   - First compare `SimulationTick`, `WarMapDraw`, and `WarUnitSummaryDraw`.
   - Use Play mode for quick iteration, but a Development Build gives cleaner numbers than Editor Play mode.

2. Add a war spatial index.
   - Maintain coarse buckets by faction and sector.
   - Use it for enemy-in-range, hearing/contact support, engineer support, and player influence checks.
   - This is the next best code change. It reduces repeated all-unit scans as unit counts rise.

3. Cache UI unit summary/grouping.
   - Rebuild summary data a few times per second or when unit counts change.
   - Avoid per-IMGUI-event LINQ, `ToList`, `OrderBy`, and repeated nearest-command scans.

4. Throttle visibility and terrain drawing.
   - Keep active combat reveal immediate.
   - Refresh broad unit vision less often or only when a unit moves enough to change its reveal footprint.
   - Continue coarse rendering when zoomed out.

5. Replace IMGUI map rendering for the battlefield.
   - Short term: draw fog/terrain into a texture or mesh layer.
   - Medium term: Unity tilemap, instanced quads, or a custom mesh renderer.
   - Keep IMGUI for prototype controls only.

6. Add a simulation budget governor.
   - Cap max active squad ticks per frame/strategic second.
   - Prioritize player-visible units, active contacts, and nearby support units.
   - Let far-away fog units run coarse tactical pulses.

7. Consider Unity Jobs/Burst later.
   - Useful only after data layout is cleaner.
   - Do not jump to Jobs before spatial indexing and render batching; that would be polishing the silver while the dining room floods.

## Risks

- The removed duplicate fog activation pass can delay a newly moved fog enemy becoming fully active by up to one strategic second. At current 5x test speed this is a small real-time delay and likely worth the saved work.
- Coarse far-zoom fog is less granular visually, by design. At closer zoom, per-cell rendering remains.
- We still need an actual Unity Profiler capture to know whether the next biggest cost is simulation, UI summary, or map drawing.

## Cleanup Performed

- No temporary files or screenshots were created.
- No old project folders were touched.

## Memory-Worthy Notes

- Trenchworks needs performance budgets treated as part of the core design. The war map target is large, so the prototype should separate:
  - active combat simulation,
  - passive/offscreen tactical simulation,
  - visible rendering,
  - remembered/fog rendering.
- IMGUI is still acceptable for prototype controls, but it should not remain the main battlefield renderer.
- The next implementation pass should prioritize spatial buckets and cached UI summaries before increasing squad counts again.

## Follow-Up Recommendations

- Run a Unity Profiler capture after this patch with the wave drill at 1x and 5x.
- Implement a `WarSpatialIndex` inside the simulation layer.
- Convert `DrawWarUnitSummary` and far-zoom squad rendering away from per-event LINQ.
- Add an in-game tiny perf readout for active units, static units, visible cells, known cells, and last sim/draw marker timings if needed.

## Blocked

- No standalone player profiling was run in this pass.
- No batchmode Unity compile was run because the project is already open in Unity Editor.
