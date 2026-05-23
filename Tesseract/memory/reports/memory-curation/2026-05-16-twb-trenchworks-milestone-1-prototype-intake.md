# TWB Trenchworks Milestone 1 Prototype Intake

## Status

Complete - 2026-05-16.

## Source Reviewed

- [[short-term/2026-05-15-twb-trenchworks-milestone-1-prototype-report]]

## Spot Check

Confirmed the prototype folder and primary files exist:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype`
- `Assets\Scenes\TrenchworksPrototype.unity`
- `Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- `Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `Assets\Scripts\Editor\TrenchworksProjectSetup.cs`
- `README.md`

Reviewed the README and searched source for the reported smoke-test, enemy-base integrity, bombardment, doctrine, command mission, supply, and fixed tick concepts.

## Promoted

- Milestone 1 prototype exists at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype`.
- Unity version used is `6000.3.8f1`.
- Prototype uses a pure C# simulation layer with Unity presentation/input.
- Fixed simulation tick is `0.1s`.
- Shippable supply categories are ammo, trench materials, rations, and medical supplies.
- War state tracks front progress, readiness, casualties, trench progress, tunnel/sap progress, bombardment progress, enemy-base integrity, doctrine, and autonomous command missions.
- Command missions include refit, push forward, extend trench, treat wounded, and prepare bombardment.
- Smoke test passed and reported:
  - first shipment tick: `45`
  - first front gain tick: `679`
  - final front progress: `67.5`
  - enemy-base integrity: `0.0`
- Sustained factory supply advantage can reduce enemy-base integrity to zero.
- The 80 percent supply / 20 percent seeded-random target is represented in the war resolver.

## Kept Report-Only

- Exact balance values.
- Exact implementation file layout beyond the primary files.
- IMGUI presentation as a final UI direction.
- The current simplified belt/transfer model as final factory identity.
- Full milestone 2 scope; that needs review before assignment.

## Warnings

- Current factory logistics are intentionally simplified.
- Current war model is a coarse strategic proof, not a finished tactical simulation.
- Current balance values prove the loop and should not be treated as final economy.
- No standalone player build has been produced.
- IMGUI is debug/prototype presentation only.

## Files Changed

- `memory/wiki/twb-trenchworks/overview.md`
- `memory/wiki/twb-trenchworks/architecture.md`
- `memory/wiki/twb-trenchworks/open-questions.md`
- `memory/wiki/twb-trenchworks/research-plan.md`
- `memory/briefs/current-twb-trenchworks-task.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`

## Remaining Blocked

- User/Bob review in Unity Editor play mode.
- Decision whether the prototype direction is worth continued investment.
- Milestone 2 scope decision: placement ergonomics, diagnostics, tests, or another narrow pass.

## Next Gate

Open the milestone 1 prototype in Unity Editor and review the loop before hydrating another implementation worker.
