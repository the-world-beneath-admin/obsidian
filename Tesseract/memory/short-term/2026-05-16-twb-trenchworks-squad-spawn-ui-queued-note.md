# TWB Trenchworks Squad Spawn UI Queued Note

## Scope

Standalone TWB Trenchworks Unity prototype.

## User Direction

Do not wire this into the live game yet. The current war-wave drill test should continue uninterrupted.

## Intended Squad Spawn UI

- Bottom rail should include one circular/minimal button per squad/team template.
- Squad buttons should read left-to-right by progression:
  - tier 1 squads on the far left;
  - higher tier squads farther right;
  - locked higher-tier squads visible but disabled or dimmed until research unlocks them.
- Clicking a squad button should open a compact lane chooser directly above that button.
- Lane chooser should contain:
  - TOP;
  - MID;
  - BOT.
- Normal final behaviour should check that the chosen lane shipping area has the resources needed for that squad.
- Lane buttons should only highlight/enable when that lane has enough stored resources.
- For the next prototype test only, resource checks should be bypassed so the player can throw squads into the war freely.

## Implementation Guardrail

The next implementation pass should not disturb the active war-wave drill unless the user explicitly asks to proceed. Do not force a Unity recompile while the user is watching the current test.

## Likely Code Touch Points Later

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Unity\PrototypeBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\Assets\Scripts\Simulation\TrenchworksSimulation.cs`
- Possibly a new squad/team catalog in `Assets\Scripts\Simulation\War\` if the current team facade is not enough.

## Follow-up Recommendation

After the current drill is observed, add the squad buttons behind a temporary prototype/debug flag:

- default drill remains readable;
- squad spawning can be enabled for manual stress testing;
- resource-gated lane highlighting can be added after free-spawn behaviour is confirmed.
