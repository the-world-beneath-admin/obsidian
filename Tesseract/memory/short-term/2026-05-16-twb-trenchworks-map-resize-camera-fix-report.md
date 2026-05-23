# TWB Trenchworks Map Resize Camera Fix Report

Date: 2026-05-16
Worker: Bob / Codex
Scope: Standalone TWB-tagged Unity 2D game, TWB Trenchworks
Project path: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`

## What Changed

- Fixed the war-map camera after the battlefield width was reduced to `800`.
- Added a dynamic minimum zoom based on the current map panel size and world dimensions so the camera cannot zoom out far enough to show off-map void.
- Centered the whole-front camera focus after choosing the safe zoom, so the visible war view starts in a cleaner playtest position instead of pinning to the top-left.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-map-resize-camera-fix-report.md`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open `Assets\Scenes\TrenchworksPrototype.unity`.
4. Press Play.
5. The war map should now clamp/zoom to the resized 800-wide battlefield instead of showing a broken off-map strip on the right.

## Whether `prototype\My project` Was Involved

No. The obsolete nested project was not touched.

## Tests / Checks Run

- Runtime source compile against Unity 6000.3.8f1 UnityEngine assemblies: passed.
- Unity editor log tail checked for `error CS`, explicit exception lines, and touched script references: no compile errors or explicit runtime exceptions found.

## Cleanup Performed

- Removed temporary compile artifacts from `Temp\CodexCompileCheck`.

## Risks

- At very wide panel sizes, the safe zoom crops more vertically than the old loose camera. That is intentional to avoid off-map void, but a later pass may want a true minimap/overview mode.
- This is a camera/layout fix only; it does not change war simulation behavior.

## Memory-Worthy Notes

- The war map is currently `800 x 600`; the UI camera now derives its minimum zoom from the live viewport instead of assuming the older wider battlefield.

## Follow-Up Recommendations

- Add a dedicated full-front overview/minimap if all three lanes must remain visible at once on every viewport.
- Consider a clean battlefield border or letterboxed overview mode if the user prefers seeing the entire map even when the panel aspect ratio is wider than the battlefield.

## Anything Blocked

- Nothing blocked.
