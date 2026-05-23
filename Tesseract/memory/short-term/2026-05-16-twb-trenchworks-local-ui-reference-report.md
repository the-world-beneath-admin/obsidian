# TWB Trenchworks Local UI Reference Report

Date: 2026-05-16

Scope: Standalone TWB-tagged game / TWB Trenchworks UI reference. This is not the main game, not Glassroot Garden, and not a shared platform/account task.

## Steam Paths Checked

- `C:\Program Files (x86)\Steam\steamapps\common` - exists; `Captain of Industry` found.
- `C:\Program Files\Steam\steamapps\common` - not present.
- `C:\SteamLibrary\steamapps\common` - not present.
- `D:\SteamLibrary\steamapps\common` - not present.
- `E:\SteamLibrary\steamapps\common` - not present.
- `F:\SteamLibrary\steamapps\common` - not present.
- `G:\SteamLibrary\steamapps\common` - not present.

Confirmed install path:

```text
C:\Program Files (x86)\Steam\steamapps\common\Captain of Industry
```

Steam manifest inspected:

```text
C:\Program Files (x86)\Steam\steamapps\appmanifest_1594320.acf
```

Manifest confirms app id `1594320`, name `Captain of Industry`, install directory `Captain of Industry`, build id `23174136`, and language `english`.

## What Was Inspected

Safe local inspection only:

- Listed the Captain of Industry install root.
- Read Steam's plaintext `appmanifest_1594320.acf`.
- Read the visible plaintext root changelog:

```text
C:\Program Files (x86)\Steam\steamapps\common\Captain of Industry\changelog.txt
```

- Listed, but did not open or copy, Steam app library artwork cached under:

```text
C:\Program Files (x86)\Steam\appcache\librarycache\1594320
```

- Listed, but did not inspect save/private content, Steam userdata folder:

```text
C:\Program Files (x86)\Steam\userdata\124474090\1594320
```

Only `remotecache.vdf` was visible there during this pass.

- Listed translation file names under:

```text
C:\Program Files (x86)\Steam\steamapps\common\Captain of Industry\Translations
```

The translation files were not read for UI mining because that would drift from practical public-facing reference into unnecessary internal text extraction.

## What Was Not Inspected

Deliberately not inspected:

- `Captain of Industry.exe`
- `UnityPlayer.dll`
- `UnityCrashHandler64.exe`
- `Captain of Industry_Data`
- `AssetBundles`
- `Maps`
- `DLCs`
- `MonoBleedingEdge`
- pathfinding/heuristics folders
- the `assemblymanual_f7da` asset-bundle-like file
- save data or other private player data
- Steam cached artwork images beyond listing filenames

No binaries were decompiled. No proprietary assets were extracted, opened for copying, or reused.

## User-Facing Files Found

In the install root:

- `changelog.txt` - plaintext, user-facing, inspected.

No obvious local manual, README, PDF, or screenshot files were found in the install root outside internal game data folders.

Steam app cache contained library/header/hero/logo artwork files for app `1594320`, but these were only identified by path and filename.

## Safe Observations From Captain of Industry

The local install was useful mainly through the changelog, which exposes user-visible UI and interaction decisions without touching internals.

Observed user-visible patterns:

- Configuration defaults matter. The changelog notes train network unload modules defaulting to a more immediately useful threshold, which reduces setup friction.
- Area ownership/readability matters. Mine towers, forestry towers, and logistic zones can be resized by dragging edges, and their full shapes highlight when the cursor is inside.
- Tooltips/search/labels are doing real labour. Cargo depot and station modules show input/output products, and product search includes trains.
- Inspectors are valuable when the world is dense. The terrain inspector shows a vertical cross-section, coloured layer bars, icons, height labels, water level, ocean indication, and contour lines.
- Summary windows can turn dangerous operations into understandable ones. The recovery save flow lists what loaded successfully and which proto IDs failed.
- Tiny icons can carry state well. Autosaves use a clock icon for clarity.
- Modifier input can accelerate expert workflows. Holding Ctrl while scrolling switches between storage tiers during placement.
- Purely visual overrides are explicitly separated from simulation state in the dolly editor, which is a good precedent for debug/visual options.

These are observations about public/user-visible behaviour surfaced by the changelog, not claims about implementation.

## Trenchworks Docs Inspected

Docs folder:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs
```

Files read:

- `milestone-1-prototype-brief.md`
- `milestone-2-playtest-stabilization-brief.md`

Project README read:

```text
C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\README.md
```

Existing Trenchworks UI notes:

- Top bar should read `TWB Trenchworks`, show tick/speed, and display base-health war tracking.
- Bottom-left circle switches between factory grid and war map.
- `W/A/S/D`, mouse wheel, and right/middle drag control pan/zoom.
- Bottom rail chooses factory tools, belt direction, assembler recipe, war doctrine, war entry lane, and war layer.
- Top tracker shows player base health, enemy base health, derived pressure, bombardment, tick, speed, and readiness.
- Right tracker switches between overview, logistics, war diagnostics, and log panels.
- Pause/speed/reset circles control simulation state.
- War map should communicate cells, obstacles, visible units, entry lanes, contact, trenches, obstacles, and base zones.
- Milestone 2 emphasizes first-open clarity: visible title, running/paused state, tick count, and obvious evidence that Play mode is alive.

## Practical Trenchworks Implications

Recommended UI direction, keeping the scope modest:

- Prioritize clear state before decorative UI. A factory/war prototype needs the title, tick, speed, pause state, current map, selected tool, selected doctrine, and supply pressure visible immediately.
- Add or strengthen hover/selection highlights for active logistics zones, depot shipping ranges, entry lanes, trenches, and contested cells. Full-shape highlighting is more useful than a tiny border when the map gets busy.
- Treat inspectors as first-class tools. A compact cell/zone inspector for terrain, supply flow, unit state, trench state, and bottleneck reason would do more for playability than a large decorative panel.
- Use defaults that create motion without configuration. First-run belts, depot shipment thresholds, and war doctrine should produce a visible supply-to-front result quickly.
- Keep right-side diagnostics dense and tabbed. Overview, Logistics, War, and Log are already sensible; resist adding more permanent panels until the prototype earns them.
- Make failure states readable. If a shipment stalls, an assembler lacks input, or units cannot advance, show one concise reason rather than a silent number.
- Separate visual/debug options from simulation state. If Trenchworks gets map overlays, cinematic views, or debug fog/visibility toggles, label them as visual/debug so they do not imply gameplay effects.
- Do not copy Captain of Industry's visuals, icons, artwork, text, or assets. The useful reference here is interaction grammar: highlighting, inspectors, readable defaults, concise summaries, and dense status surfaces.

## Risks And Limits

- Local inspection did not include live play of Captain of Industry, screenshots, or manuals, so observations are limited to installed-file structure and public changelog text.
- Steam cached artwork exists locally, but it was not opened or reused.
- Translation files may contain UI strings, but reading them was unnecessary for this bounded task and could encourage overly derivative UI borrowing.
- The Trenchworks docs currently describe intended UI structure, but not a dedicated detailed UI style guide. The next UI pass should turn those notes into a small in-project UI checklist before adding more surfaces.

## Cleanup

No temporary files, screenshots, extracted assets, or scratch folders were created.
