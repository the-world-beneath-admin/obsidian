# TWB Creature Sprite Sheets Overview

## Status

Complete art-pipeline lane - created 2026-05-12; automation paused 2026-05-17 after all queue rows reached `QA Passed`.

## Scope

This lane covers Unity-ready 4-direction creature walk sprite sheets for the Tier 1 pet/card-art system in the main **The World Beneath** Unity project.

Project source:

```text
C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype
```

## Memory Items

- Fact - The source creature art hierarchy is `.md\T1_Creature_Art_Prompt_System\affinities\`.
- Fact - The sprite-sheet queue contains `117` family triad chunks of `3` creatures each.
- Fact - As of `RO-13` on 2026-05-17, `CHUNK_QUEUE.md` has no remaining `Pending` rows; all `117` family triad chunks are marked `QA Passed`.
- Decision - The recurring sprite-sheet automation `twb-sprite-sheet-triad-runner` is paused because the Tier 1 creature walk sprite-sheet queue is complete.
- Fact - Chunks `AE-01`, `AE-02`, and `AE-03` are complete and marked `QA Passed`.
- Fact - Chunks `AE-04` / `arcane-engineering` / `grassland` are now complete and marked `QA Passed` (atk-vaneclaw-hopper, def-kiteplate-prairie-dog, util-weatherbell-lark).
- Fact - Chunks `AE-05` / `arcane-engineering` / `industrial` are now complete and marked `QA Passed` (atk-scrawlbit-mouse, def-bracketback-pillbug, util-gaugewhisper-moth).
- Fact - `AE-06` / `arcane-engineering` / `marine` is complete and marked `QA Passed` (atk-clampclaw-crab, def-barnacle-bracket-snail, util-buoykey-plover).
- Fact - `AE-07` / `arcane-engineering` / `park` is complete and marked `QA Passed` (atk-keybill-duck, def-coinplate-turtle, util-fountainchime-sparrow).
- Fact - Special companion `Stanly` walk sheet is complete in `affinities/special/ephemrial_spirit/`.
- Fact - `AE-08` / `arcane-engineering` / `rural_agricultural` is complete and queue-updated as `QA Passed` with `atk-crankspur-rooster`, `def-chaffplate-goat`, and `util-pulleywhisker-mouse`.
- Fact - `AE-09` / `arcane-engineering` / `temperate_forest` is complete and queue-updated as `QA Passed` with `atk-rulerbite-squirrel`, `def-stakeback-badger`, and `util-plumbline-wren`.
- Fact - `AE-10` through `AE-13` are complete and queue-updated as `QA Passed`; Arcane Engineering is now complete through `AE-13`.
- Fact - Special companion `Chuck` walk sheet is complete in `affinities/special/ephemrial_spirit/`.
- Fact - Special companion `Nova` walk sheet is complete in `affinities/special/ephemrial_spirit/`.
- Fact - `AF-04` / `arcane-fighting` / `grassland` is complete and marked `QA Passed` with `atk-shearsigil-redsigil`, `def-huskward-redsigil`, and `util-chantstep-redsigil`.
- Fact - `AF-05` / `arcane-fighting` / `industrial` is complete and marked `QA Passed` with `atk-cutwire-rat`, `def-plateback-rat`, and `util-marktail-rat`.
- Fact - `AF-05` required one regeneration for `util-marktail-rat` because the first pass drifted toward a heavier armored silhouette.
- Fact - `AF-06` / `arcane-fighting` / `marine` is complete and marked `QA Passed` with `atk-shearclaw-tidesigil`, `def-shellward-tidesigil`, and `util-driftstep-tidesigil`.
- Fact - `AF-07` / `arcane-fighting` / `park` is complete and marked `QA Passed` with `atk-glaivewing-goose`, `def-wardbreast-goose`, and `util-patterncall-goose`.
- Fact - `AF-08` / `arcane-fighting` / `rural_agricultural` is complete and marked `QA Passed` with `atk-lancehorn-goat`, `def-wardhorn-goat`, and `util-bellmark-goat`.
- Fact - `AF-09` / `arcane-fighting` / `temperate_forest` is complete and marked `QA Passed` with `atk-shearclaw-wardscar`, `def-knotguard-wardscar`, and `util-slipsigil-wardscar`.
- Fact - `CU-10` / `cunning` / `tropical_forest` is complete and marked `QA Passed` with `atk-spurpetal-mantis`, `def-cupbract-toad`, and `util-pollenhush-lanternfly`.
- Fact - `CU-11` / `cunning` / `tundra` is complete and marked `QA Passed` with `atk-thawlure-ermine`, `def-steamblind-ptarmigan`, and `util-ventwink-vole`.
- Fact - `CU-12` / `cunning` / `urban_commercial` is complete and marked `QA Passed` with `atk-cuttertag-tatterling`, `def-wraphush-tatterling`, and `util-shelfskip-tatterling`.
- Fact - `CU-13` / `cunning` / `urban_residential` is complete and marked `QA Passed` with `atk-veinlick-duskfed`, `def-curtaincoil-duskfed`, and `util-sillskulk-duskfed`.
- Fact - `CY-01` / `cybernetics` / `boreal_forest` is complete and marked `QA Passed` with `atk-spurjack-sable`, `def-barkplate-beaver`, and `util-pinepulse-marten`.
- Fact - `CY-02` / `cybernetics` / `desert` is complete and marked `QA Passed` with `atk-sunspur-jackrabbit`, `def-heatplate-tortoise`, and `util-relaytail-kit-fox`.
- Fact - `CY-03` / `cybernetics` / `freshwater` is complete and marked `QA Passed` with `atk-splicejaw-pike`, `def-brakelid-beaver`, and `util-currentfin-otter`.
- Fact - `CY-04` / `cybernetics` / `grassland` is complete and marked `QA Passed` with `atk-sparkspur-meadowlark`, `def-insulator-prairie-dog`, and `util-fenceping-cricket`.
- Fact - `CY-05` / `cybernetics` / `industrial` is complete and marked `QA Passed` with `atk-needlebit-shrew`, `def-patchplate-roach`, and `util-linecall-moth`.
- Fact - `CY-06` / `cybernetics` / `marine` is complete and queue-updated as `QA Passed` with `atk-saltneedle-tern`, `def-hullpatch-crab`, and `util-buoyping-gull`.
- Fact - `CY-07` / `cybernetics` / `park` is complete and queue-updated as `QA Passed` with `atk-curbneedle-squirrel`, `def-benchplate-turtle`, and `util-pathping-sparrow`.
- Fact - `CY-08` / `cybernetics` / `rural_agricultural` is complete and queue-updated as `QA Passed` with `atk-needletag-rooster`, `def-gateplate-goat`, and `util-silochirp-swallow`.
- Fact - `CY-09` / `cybernetics` / `temperate_forest` is complete and queue-updated as `QA Passed` with `atk-lensjaw-fox`, `def-barkpatch-porcupine`, and `util-tripwire-wren`.
- Fact - `CY-10` / `cybernetics` / `tropical_forest`, `CY-11` / `cybernetics` / `tundra`, `CY-12` / `cybernetics` / `urban_commercial`, `CY-13` / `cybernetics` / `urban_residential`, and `FA-01` / `faith` / `boreal_forest` are complete and marked `QA Passed`.
- Fact - `FA-02` / `faith` / `desert` is complete and marked `QA Passed` with `atk-sunlash-gecko`, `def-shelterback-gecko`, and `util-coolveil-gecko`.
- Fact - `FA-03` / `faith` / `freshwater` is complete and marked `QA Passed` with `atk-needlefont-darter`, `def-basinback-terrapin`, and `util-blessing-skater`.
- Fact - `FA-04` / `faith` / `grassland` is complete and marked `QA Passed` with `atk-thornhalo-hare`, `def-basinback-lamb`, and `util-dewsong-lark`.
- Fact - `FA-05` / `faith` / `industrial` is complete and marked `QA Passed` with `atk-censer-spit-slagling`, `def-bastion-drip-slagling`, and `util-wick-scribe-slagling`.
- Fact - `FA-06` / `faith` / `marine` is complete and marked `QA Passed` with `atk-titheclaw-hermit`, `def-wardshell-limpet`, and `util-prayerfrond-kelp`.
- Fact - `FA-07` / `faith` / `park` is complete and marked `QA Passed` with `atk-dawnspitter-frog`, `def-basin-toad`, and `util-coinsnail`.
- Fact - `FA-08` / `faith` / `rural_agricultural` is complete and marked `QA Passed` with `atk-spurbeak`, `def-woolward`, and `util-wickmoth`.
- Fact - `FA-09` / `faith` / `temperate_forest` is complete and marked `QA Passed` with `atk-candlehorn-pricket`, `def-shrineback-hind`, and `util-bellstep-fawn`.
- Fact - `FA-10` / `faith` / `tropical_forest`, `FA-11` / `faith` / `tundra`, `FA-12` / `faith` / `urban_commercial`, and `FA-13` / `faith` / `urban_residential` are complete and marked `QA Passed`.
- Fact - `MA-01` / `magic` / `boreal_forest`, `MA-02` / `magic` / `desert`, and `MA-03` / `magic` / `freshwater` are complete and marked `QA Passed`.
- Fact - `MA-04` / `magic` / `grassland` is complete and marked `QA Passed` with `atk-shardbloom-thistlekin`, `def-wardstem-thistlekin`, and `util-sootpollen-thistlekin`.
- Fact - `MA-05` / `magic` / `industrial` is complete and marked `QA Passed` with `atk-sparkgnaw-tenrec`, `def-boilerback-roach`, and `util-chalkwing-moth`.
- Fact - `MA-06` / `magic` / `marine` is complete and marked `QA Passed` with `atk-sparkspine-shellkin`, `def-refractshell-shellkin`, and `util-wakeglow-shellkin`.
- Fact - `MA-07` / `magic` / `park` is complete and marked `QA Passed` with `atk-coinpeck-starling`, `def-markerback-toad`, and `util-ribbonmote-firefly`.
- Fact - `MA-08` / `magic` / `rural_agricultural` is complete and marked `QA Passed` with `atk-spurhex-rooster`, `def-baleback-toad`, and `util-cornsilk-caddisfly`.
- Fact - `MA-09` / `magic` / `temperate_forest` is complete and marked `QA Passed` with `atk-sparkclaw-cairnroot`, `def-wardback-cairnroot`, and `util-mosshush-cairnroot`.
- Fact - `MA-10` / `magic` / `tropical_forest` is complete and marked `QA Passed` with `atk-stormthread-spitter`, `def-basinweb-warder`, and `util-hushlace-dewspinner`.
- Fact - `MA-11` / `magic` / `tundra` is complete and marked `QA Passed` with `atk-splinterpika`, `def-cairnback-vole`, and `util-wickwhisk-lemming`.
- Fact - `MA-12` / `magic` / `urban_commercial` and `MA-13` / `magic` / `urban_residential` are complete and marked `QA Passed`.
- Fact - `MI-01` / `might` / `boreal_forest` is complete and marked `QA Passed` with `atk-ripsnout`, `def-knotback`, and `util-mireturn`.
- Fact - `MI-02` / `might` / `desert` is complete and marked `QA Passed` with `atk-briartusk-boar`, `def-thatchback-bulwark`, and `util-quillwhistle-degu`.
- Fact - `MI-07` / `park`, `MI-08` / `rural_agricultural`, `MI-09` / `temperate_forest`, and `MI-10` / `tropical_forest` are complete and marked `QA Passed`.
- Fact - `MI-11` / `might` / `tundra`, `MI-12` / `might` / `urban_commercial`, and `MI-13` / `might` / `urban_residential` are complete and marked `QA Passed`; Might affinity is complete through `MI-13`.
- Fact - `MN-01` / `mind` / `boreal_forest` is complete and marked `QA Passed` with `atk-needleflash-ermine`, `def-barkguard-porcupine`, and `util-hushjay`.
- Fact - `MN-02` / `mind` / `desert` is complete and marked `QA Passed` with `atk-glassfang-sidewinder`, `def-sunshell-tortoise`, and `util-hushcall-sandgrouse`.
- Fact - `MN-03` / `mind` / `freshwater` is complete and marked `QA Passed` with `atk-ripplejaw-pike`, `def-siltshell-terrapin`, and `util-reedcall-grebe`.
- Fact - `MN-04` / `mind` / `grassland` is complete and marked `QA Passed` with `atk-bristlewing-shrike`, `def-thatchmantle-grouse`, and `util-hushwhistle-lark`.
- Fact - `MN-05` / `mind` / `industrial` is complete and marked `QA Passed` with `atk-alarmtooth-rat`, `def-braceback-rat`, and `util-signalwhisk-rat`.
- Fact - `MN-06` / `mind` / `marine` through `MN-12` / `mind` / `urban_commercial` are complete and marked `QA Passed`.
- Fact - `MN-13` / `mind` / `urban_residential` is complete and marked `QA Passed` with `atk-needlemark-wasp`, `def-nestplate-wasp`, and `util-porchsignal-wasp`.
- Fact - Mind affinity is complete through `MN-13`.
- Fact - `RO-01` / `robotics` / `boreal_forest` is complete and marked `QA Passed` with `atk-cutter-rig`, `def-brace-drum`, and `util-relay-spool`.
- Fact - `RO-02` / `robotics` / `desert` is complete and marked `QA Passed` with `atk-sawjaw-scarab`, `def-plateback-scarab`, and `util-relayback-scarab`.
- Fact - `RO-03` / `robotics` / `freshwater` is complete and marked `QA Passed` with `atk-rotor-pike`, `def-anchor-shell`, and `util-beacon-skater`.
- Fact - `RO-04` / `robotics` / `grassland`, `RO-05` / `robotics` / `industrial`, and `RO-06` / `robotics` / `marine` are complete and marked `QA Passed`.
- Superseded - `RO-07` / `robotics` / `park` was previously blocked mid-triad; it is now complete and marked `QA Passed`.
- Fact - `RO-07` through `RO-13` are complete and marked `QA Passed`; Robotics is complete through `RO-13`.
- Superseded - The next recommended production chunk was `RO-11` / `robotics` / `tundra`; that gate has since passed.
- Superseded - The next pending triad previously pointed at `RO-04` / `robotics` / `grassland`; that gate has since passed.
- Superseded - The next pending triad previously pointed at `MN-06` / `mind` / `marine`; that gate has since been overtaken by the robotics queue.
- Superseded - The next recommended production chunk was `FA-02` / `faith` / `desert`; that gate has since passed.
- Superseded - The next recommended production chunk was `MA-01` / `magic` / `boreal_forest`; that gate has since passed.
- Superseded - The next recommended production chunk was `MA-08` / `magic` / `rural_agricultural`; that gate has since passed.
- Decision - Final walk sheets are filed beside their matching card-art PNG in the existing affinity/biome hierarchy.
- Decision - Future sprite-sheet workers should report to `memory/short-term/`.
- Decision - The automation processes one family triad package per hourly run.
- Decision - The automation runs from only `C:\Users\yrred\Desktop\Obsidian\Tesseract` and uses a singleton lock file to prevent duplicate concurrent runs.
- Decision - The automation treats locks as stale/orphaned at 90 minutes and refreshes a heartbeat during healthy long runs.
- Decision - Any temporary solid/chroma matte should use magenta `#FF00FF`, never lime/green.
- Decision - A finishing pass is required to remove matte spill, cutout halos, and outline artifacts before final QA.
- Warning - For robotics sheets, soft magenta removal before repack is safer than a direct hard repack because the direct path can preserve purple edge contamination.
- Source: [[short-term/2026-05-12-twb-creature-spritesheets-working-window-intake]]
- Source: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\ImageCreatorPipeline\17_CreatureWalkSpriteSheets\CHUNK_QUEUE.md`
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-mn-01]]
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-mn-02]]
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-mn-03]]
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-mn-04]]
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-mn-05]]
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-mn-13]]
- Source: [[short-term/2026-05-17-twb-creature-spritesheet-auto-ro-03]]
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-ro-02]]
- Source: [[short-term/2026-05-16-twb-creature-spritesheet-auto-ro-01]]
- Source: [[short-term/2026-05-17-twb-creature-spritesheet-auto-ro-13]]

## Completed Production Rhythm

The recurring production run is complete and paused. If the automation is ever reactivated for a new batch, preserve these proven rules:

- Work one family triad at a time.
- Acquire the singleton lock before selecting a queue item.
- Generate and repack one creature at a time.
- Use magenta temporary matte only if a solid/chroma background is needed.
- Run the finishing pass before accepting final transparent output.
- QA each creature before moving to the next.
- Update `CHUNK_QUEUE.md` only after all three creatures in the family triad pass QA.

## Next Gate

No further automated sprite-sheet production is needed for this queue. Optional follow-up: run a Unity import/playback spot check for the final robotics sheets, especially `RO-13` / `robotics` / `urban_residential`.
