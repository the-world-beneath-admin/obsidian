# TWB Trenchworks Visual Quality Pass Report

Date: 2026-05-16

## Scope

Standalone TWB-tagged game: TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

## What Changed

- Stylized trench rendering so each trench tile now has clearer rim/sided-wall cues, a darker middle channel, and a center node on intersections.
- Kept supply-connected trench strips visible after the new trench channel detail is drawn.
- Added render-side smoothing for visible war units so the simulation can still tick by grid cell while unit markers glide toward their current cell position.
- Reduced non-combat unit influence patch opacity so the screen is less cluttered during scouting.
- Changed reset/startup war layer to `Surface` instead of `All`, so the wave drill no longer opens with every diagnostic overlay visible.
- Limited the squad intent path line to the selected squad only, instead of drawing scouting/intent lines for every squad leader.

## Files Touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-visual-quality-pass-report.md`

## How To Run It In Unity Hub

1. Open Unity Hub.
2. Open `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
3. Open or confirm scene `Assets\Scenes\TrenchworksPrototype.unity`.
4. Press Play.
5. The wave drill should start on the normal Surface view. Use `LYR`/`FLD` only when debug field overlays are needed.

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
  - Current open editor imported `PrototypeBootstrap.cs`, booted `TrenchworksPrototype`, and logged `PrototypeBootstrap.Awake` plus first `OnGUI` frame.
  - No C# compile error was found in the relevant log scan.

## Cleanup Performed

- No temporary files, screenshots, or batchmode logs were created during this pass.

## Risks

- The smoothing is render-only. It improves visual jitter without changing simulation movement; if the simulation itself stalls, this will not hide or fix the underlying AI behavior.
- Trench styling is still immediate-mode rectangle art. It is more readable now, but final art or a tile/sprite pass may eventually replace it.
- Full Unity batchmode smoke was not run because an active Unity editor instance is already open on the project.

## Memory-Worthy Notes

- Normal play should default to `WarLayer.Surface`; `WarLayer.All` is useful for diagnostics but visually too noisy for playtesting.
- Squad intent lines are better as selected-unit diagnostics than always-on battlefield decoration.
- Render interpolation can be used safely for readability as long as simulation positions remain authoritative.

## Follow-Up Recommendations

- Live Play review should check whether the new trench channels make the trench middle and sides readable at common zoom levels.
- If jitter remains, separate likely causes into simulation stutter, GUI repaint cost, and per-unit decision cadence rather than guessing from the visual result.
- Consider an optional UI toggle for debug influence patches, since they are useful while tuning AI but distracting during normal play.

## Anything Blocked

- Batchmode smoke testing was skipped because Unity is already open on this project. The source-level compiler check passed; live Play confirmation remains the next useful check.
