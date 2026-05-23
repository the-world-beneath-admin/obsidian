# TWB Trenchworks Worker Decommission Intake

## Status

Complete - 2026-05-17.

## Source Reviewed

- [[short-term/2026-05-17-twb-trenchworks-worker-final-decommission-report]]

## Scope

Standalone TWB Trenchworks Unity 2D project under The World Beneath umbrella.

## Promoted

- Active Unity project is `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks`.
- Canonical scene is `Assets\Scenes\TrenchworksPrototype.unity`.
- The active Unity project folder is not a git repository.
- `SampleScene.unity` still exists, so workers must verify the prototype scene before Play Mode testing.
- The old `prototype` / `prototype\My project` confusion is obsolete and should not be resurrected.
- Play Mode has visibly run the prototype in the correct project before.
- The final icon-wired UI still needs a live editor/user visual review.
- V3 interface/logistics icon package has `4/4` packs and `64` labelled icons.
- Bottom/action UI controls now use V3 icon art with hover tooltips.
- Unity batchmode icon validation passed on 2026-05-17.
- Unity simulation smoke passed on 2026-05-17 after the latest integration.
- The first-pass war-side asset package is prototype-ready but not final runtime sprite/tilemap/animation integration.
- The current editor icon loading path uses `Application.dataPath`, which is acceptable for editor Play Mode but not final packaged builds.

## Kept Report-Only

- Exact file-count snapshots for all generated art outputs.
- One-off AI tuning values and current wave-drill balance numbers.
- Rejected/candidate sprite sheet details not separately approved.
- Batchmode licensing-token noise beyond the warning that it appeared while commands still returned `0`.

## Warnings

- The project needs a live Play Mode review before the next implementation expansion.
- Do not treat batchmode validation as visual UI approval.
- Do not assume the V3 asset package means battlefield runtime sprite/tilemap rendering is complete.
- Consider putting the active Unity project under git before another large pass.

## Files Changed

- `memory/briefs/current-twb-trenchworks-task.md`
- `memory/briefs/current-game-dev-task.md`
- `memory/wiki/twb-trenchworks/overview.md`
- `memory/wiki/twb-trenchworks/architecture.md`
- `memory/wiki/twb-trenchworks/open-questions.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\twb-trenchworks-worker\HYDRATION_PROMPT.md`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\twb-trenchworks-worker.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\twb-trenchworks-playtest-worker.toml`

## Remains Blocked

- Live editor/user visual review of icon-wired UI.
- Packaged-build asset pipeline choice.
- Battlefield sprite/tile renderer integration.
- Git/source-control baseline for the active Unity project.

## Next Gate

Hydrate a fresh visible Trenchworks worker window with:

```text
C:\Users\yrred\Documents\New project 2\twb-trenchworks-worker\HYDRATION_PROMPT.md
```

The next worker should perform a visible Unity Play Mode review first. If clean, it should propose the next narrow battlefield renderer pass instead of adding it immediately.
