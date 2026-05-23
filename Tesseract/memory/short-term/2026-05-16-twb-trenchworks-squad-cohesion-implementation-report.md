# TWB Trenchworks Squad Cohesion Implementation Report

Date: 2026-05-16

Scope: standalone TWB Trenchworks Unity 2D prototype at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.

This pass did not touch the main TWB Unity project, Glassroot Garden, Alchemy Lab, marketing, shared-platform, or sprite-sheet lanes.

## What changed

- Added structural squad identity to war units:
  - `SquadId`
  - `LeaderId`
  - `FormationIndex`
  - last movement direction for less jittery movement scoring.
- Wired both starter war units and wave-drill units into 4-unit squads led by a `Command` unit.
- Changed war-agent ticking so commanders update before squad followers.
- Added a 15-cell commander cohesion radius:
  - followers outside the radius move back toward their leader/formation;
  - followers avoid moves that would keep or push them outside the radius;
  - if the commander is dead, the follower loses the tether and can behave more chaotically.
- Added leader waiting:
  - commanders pause scouting when their squad is close to exceeding cohesion range.
- Tuned scouting:
  - leaders still prefer forward movement;
  - movement is less dominated by per-unit random noise;
  - straight-line forward movement is still discouraged;
  - cover has stronger scouting value, ready for richer natural obstacle cover.
- Reduced the default Play Mode wave-drill speed from `20x` to `5x` so motion is easier to read.
- Extended the editor smoke test with a commander-radius assertion.

## Files touched

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-squad-cohesion-analysis.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-16-twb-trenchworks-squad-cohesion-implementation-report.md`

## Tests/checks run

- Unity/Roslyn runtime source compile using the project `Assembly-CSharp.rsp`: passed.
- Unity/Roslyn editor source compile using `Assembly-CSharp-Editor.rsp` with the temporary runtime reference: passed.
- No-window deterministic squad cohesion smoke: passed.
  - `followers=162`
  - `maxLeaderDistance=13`
  - `playerLeaderX=189.4`
  - `enemyLeaderX=813.4`
  - `pulses=14`
  - `contacts=1`
  - `trenches=3`

## Cleanup performed

- Removed temporary compile/smoke harness under `Temp\CodexCompileCheck`.
- Did not write to Obsidian wiki/index/hot/log.
- Closed the analysis worker after receiving its report.

## Risks

- This is still a prototype squad model, not the final team-order system.
- Commanders now pause for stragglers, which improves squad shape but may make some squads advance more cautiously.
- The 15-cell leash is strict while commanders live; future unit roles may need exceptions for scouts, runners, or broken morale.
- The visual feel still needs live Play Mode review because source-level smoke can prove behavior, not aesthetics.

## Memory-worthy notes

- Fact - Visible war units now have structural squad identity instead of only implied spawn grouping.
- Fact - Live commanders enforce a 15-cell follower radius; dead commanders release the squad into looser behavior.
- Fact - Play Mode wave drill now defaults to `5x` rather than `20x` for visual readability.
- Warning - The current movement is still grid-step based; true smooth motion would require a render interpolation layer, not just simulation tuning.

## Follow-up recommendations

- Watch the live drill and confirm whether `5x` is the right default viewing speed.
- Add role-specific squad exceptions later: scout teams can spread wider, assault teams can surge briefly, engineers should stay close to cover-building targets.
- After natural obstacles are implemented, tune cover weights again so squads prefer covered forward routes without becoming timid.
- Consider a visual line or subtle squad grouping overlay if the right-side unit summary becomes hard to read.

## Anything blocked

Full Unity batchmode/editor automation was not launched because the live Unity editor is already open on the project. Source-level runtime/editor compiles and deterministic no-window smoke passed.
