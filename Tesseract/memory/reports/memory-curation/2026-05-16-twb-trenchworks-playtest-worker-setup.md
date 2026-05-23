# TWB Trenchworks Playtest Worker Setup

## Status

Complete - 2026-05-16.

## Scope

Standalone Unity 2D TWB Trenchworks lane.

## User Signal

The user imported the game into Unity Hub, pressed Play, and nothing visibly happened, though many assets appeared to load.

## Review

Reviewed current Trenchworks memory, the milestone 1 intake, the prototype README, Unity scene, bootstrap script, editor setup script, and project folders.

Confirmed:

- intended prototype project: `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype`
- intended scene: `Assets\Scenes\TrenchworksPrototype.unity`
- scene contains `Trenchworks Prototype Bootstrap`
- `PrototypeBootstrap` draws the prototype through IMGUI
- a nested default Unity project exists at `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\prototype\My project`
- the nested project appears to contain default URP/sample-scene assets and is a likely cause of the "Play did nothing" experience if opened in Unity Hub

## What Changed

- Created `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\docs\milestone-2-playtest-stabilization-brief.md`.
- Created project worker folder `C:\Users\yrred\Documents\New project 2\twb-trenchworks-playtest-worker`.
- Created hydration prompt `C:\Users\yrred\Documents\New project 2\twb-trenchworks-playtest-worker\HYDRATION_PROMPT.md`.
- Created custom agent `C:\Users\yrred\Documents\New project 2\.codex\agents\twb-trenchworks-playtest-worker.toml`.
- Updated the active Trenchworks task brief for play-mode entry stabilization.
- Updated hot/index/log and the multi-agent role list.

## Worker Scope

The next worker should first make Unity Play mode visibly show the Trenchworks prototype from a cold Unity Hub open. Only after that may it perform small diagnostics or placement-ergonomics stabilization.

## Memory Promoted

- The user experienced a Unity Hub / Play mode entry-point failure on the Trenchworks prototype.
- A nested default Unity project at `prototype\My project` exists and may be the cause.
- Next Trenchworks gate is play-mode entry stabilization, not new game systems.

## Remains Blocked

- Actual Unity Editor verification has not been performed by Bob in this setup pass.
- The worker must confirm which project path Unity Hub opened.
- The nested project should not be deleted without user/Bob approval.

## Next Gate

Hydrate `twb-trenchworks-playtest-worker` and have it fix the entry-point problem first.
