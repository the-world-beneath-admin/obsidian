# 2026-05-15 TWB Trenchworks Milestone 1 Prototype Report

## Scope

Standalone TWB-tagged Unity 2D game under The World Beneath umbrella.

This is not the main Unity game, not Glassroot Garden, not another World Key, and not a shared platform/account system.

## What changed

- Created the first Unity project under `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype`.
- Added a pure C# simulation layer for the factory and war state.
- Added a starter factory proof layout with edge resource nodes, extractors, belts, assemblers, storage-capable entities, and a shipping depot.
- Added shippable supply categories: ammo, trench materials, rations, and medical supplies.
- Added fixed-step simulation ticking at `0.1s` per tick.
- Added a two-faction war simulation with front progress, readiness, casualties, trench progress, tunnel/sap progress, bombardment progress, enemy-base integrity, doctrine, and autonomous command missions.
- Added an IMGUI Unity presenter with a factory grid view and a war tactical/status view.
- Added battle log text explaining supply, readiness, random friction, command mission choices, front changes, bombardment, and enemy-base damage.
- Added an editor smoke-test method that verifies the factory-to-war loop reaches enemy-base annihilation.

## Files touched

Primary prototype files:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\README.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\Assets\Scenes\TrenchworksPrototype.unity`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\Assets\Scripts\Editor\TrenchworksProjectSetup.cs`

Unity-created project support files:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\Packages\manifest.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\Packages\packages-lock.json`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\ProjectSettings\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\UserSettings\`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\Library\`
- Unity `.meta` files under `Assets\`

Report:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-15-twb-trenchworks-milestone-1-prototype-report.md`

## How to run it

1. Open Unity Hub or Unity Editor.
2. Open project folder: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype`.
3. Use Unity version `6000.3.8f1`.
4. Open scene: `Assets\Scenes\TrenchworksPrototype.unity`.
5. Press Play.

The prototype starts with a working proof layout. Use Factory / War Map to switch screens, Reset Scenario to restore the starter line, doctrine buttons to steer command behavior, and placement controls to add or erase grid entities.

## Tests/checks run

Unity project creation:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -batchmode -quit -createProject 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype'
```

Scene generation and compile:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype' -batchmode -quit -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.CreatePrototypeScene
```

Simulation smoke test:

```powershell
& 'C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe' -projectPath 'C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype' -batchmode -quit -executeMethod TWB.Trenchworks.Editor.TrenchworksProjectSetup.RunSimulationSmokeTest
```

Smoke-test result:

- Passed.
- First shipment tick: `45`.
- First front gain tick: `679`.
- Final front progress: `67.5`.
- Enemy-base integrity: `0.0`.

Implementation issue caught and fixed during smoke testing:

- Assemblers were initially transferring raw inputs onto output belts before crafting.
- Assemblers could also overfill with one input type and block the second ingredient.
- Both issues were fixed by restricting assembler output transfers to supply crates and adding a small per-input buffer limit.

## Cleanup performed

- Removed the throwaway Unity smoke-test log.
- Removed Unity-generated `prototype\Logs\` after checks.
- No screenshots, scratch scripts, or temporary external files were left behind.
- Permanent Obsidian memory was not updated.

## Risks

- The factory logistics are intentionally simplified. Belts move small item counts cell-to-cell, with no splitters, inserters, lane logic, or rich bottleneck tooling yet.
- The war model is a coarse strategic proof, not a finished tactical simulation.
- Balance values are tuned to prove the loop, not to represent a final game economy.
- The UI is IMGUI debug/prototype presentation, suitable for milestone 1 but not a final UI direction.
- No standalone player build was created; verification was through Unity batch compile/scene generation and simulation smoke test.

## Memory-worthy notes

- Milestone 1 now has a runnable Unity project at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype`.
- The starter loop demonstrates factory shipping affecting readiness, casualties, front movement, bombardment progress, and enemy-base integrity.
- Enemy-base integrity can reach zero through sustained supply advantage.
- The simulation keeps gameplay state in plain C# classes, with Unity acting as presentation and input surface.
- Command behavior is doctrine-influenced but autonomous: command units choose refit, push forward, extend trench, treat wounded, or prepare bombardment from supply/readiness state.
- The 80 percent supply / 20 percent seeded random variance target is represented in the war resolver.

## Follow-up recommendations

- Keep the next pass narrow: improve player-built placement ergonomics and diagnostics before adding new systems.
- Add explicit inserter/adjacent-transfer devices only after deciding whether they are truly needed for Trenchworks identity.
- Add pure C# edit-mode tests for factory recipes, transfer rules, shipping, command mission selection, and seeded war outcomes.
- Add a small visual legend or hover details if Bob approves moving beyond debug UI.
- Do not add multiplayer, shared account/pet integration, power, fluids, trains, robots, circuits, blueprints, or campaign structure until this loop is reviewed.

## Anything blocked

Nothing blocked.

Unity tooling was available locally at:

```text
C:\Program Files\Unity\Hub\Editor\6000.3.8f1\Editor\Unity.exe
```
