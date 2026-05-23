# TWB Creature Sprite Sheet Decisions

## Active Decisions

- Decision - Final walk sheets are filed beside their matching card-art PNG in the existing `.md\T1_Creature_Art_Prompt_System\affinities\<affinity>\<biome>\` hierarchy, not in a central animation folder.
- Source: [[short-term/2026-05-12-twb-creature-spritesheets-working-window-intake]]

- Decision - Walk sheet naming strips only a terminal version suffix like `-v2`, then appends `-walk-4dof-1024`.
- Source: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\CREATURE_WALK_SPRITESHEET_USAGE.md`

- Decision - Standard sheet contract is `1024x1024`, `4x4`, `256x256` cells, row order `down`, `left`, `right`, `up`, with `4` frames per direction.
- Source: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\CREATURE_WALK_SPRITESHEET_USAGE.md`

- Decision - Unity metadata should use `Sprite (2D and UI)`, `Multiple`, bottom-center pivot `{x: 0.5, y: 0.08}`, no mipmaps, no compression, and alpha transparency enabled.
- Source: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\CREATURE_WALK_SPRITESHEET_USAGE.md`

- Decision - Fish, hover, or non-walking creatures may use a walk-equivalent animation while preserving the same `4`-direction sheet layout until runtime semantics are changed deliberately.
- Source: [[short-term/2026-05-12-twb-creature-spritesheets-working-window-intake]]

- Decision - Existing folder names should be preserved unless a deliberate migration is planned, even when they contain misspellings such as `ephemrial_spirit`.
- Source: [[short-term/2026-05-12-twb-creature-spritesheets-working-window-intake]]

- Decision - `AE-04` / `arcane-engineering` / `grassland` is complete, marked `QA Passed`, and queue-updated in `CHUNK_QUEUE.md`.
- Source: [[short-term/2026-05-12-twb-creature-spritesheet-ae-04]]

- Decision - The recurring sprite-sheet automation processes exactly one family triad package per hourly run.
- Source: User request, 2026-05-12.

- Decision - `AE-06` / `arcane-engineering` / `marine` is complete and marked `QA Passed`, and `CHUNK_QUEUE.md` was updated after all three creatures passed mechanical QA, finishing pass, and visual checks.
- Source: [[short-term/2026-05-12-twb-creature-spritesheet-auto-ae-06]]

- Decision - `AE-07` / `arcane-engineering` / `park` is complete and marked `QA Passed`, and `CHUNK_QUEUE.md` was updated after duck and turtle reuse plus newly QA-passed `util-fountainchime-sparrow` passed mechanical, finishing, and visual checks.
- Source: [[short-term/2026-05-12-twb-creature-spritesheet-auto-ae-07]]

- Decision - `Stanly` (`special` / `ephemrial_spirit`) has a completed walk sheet with `QA Passed` checks and matching `.meta`/`.manifest.json`.
- Source: [[short-term/2026-05-12-twb-creature-spritesheet-stanly]]

- Decision - `AE-07` / `arcane-engineering` / `park` is complete and marked `QA Passed`; the queue update happened after a blocked first run was resolved in a rerun.
- Source: [[short-term/2026-05-12-twb-creature-spritesheet-auto-ae-07]]

- Decision - `AE-08` / `arcane-engineering` / `rural_agricultural` is complete and marked `QA Passed`; queue update happened after `atk-crankspur-rooster`, `def-chaffplate-goat`, and `util-pulleywhisker-mouse` passed mechanical QA, finishing, and visual checks.
- Source: [[short-term/2026-05-12-twb-creature-spritesheet-auto-ae-08-complete]]

- Decision - `AE-09` / `arcane-engineering` / `temperate_forest` is complete and marked `QA Passed` with `atk-rulerbite-squirrel`, `def-stakeback-badger`, and `util-plumbline-wren`; the queue was updated after repack and finishing-pass visual checks.
- Source: [[short-term/2026-05-12-twb-creature-spritesheet-auto-ae-09-complete]]

- Decision - Any temporary solid/chroma matte used during sprite generation or cleanup should be flat magenta `#FF00FF`, not lime/green.
- Source: User request, 2026-05-12.

- Decision - Each creature requires a finishing pass to remove matte spill, cutout halos, and outline artifacts before final QA.
- Source: User request, 2026-05-12.

- Superseded - The hourly sprite-sheet automation previously used only one configured workspace at `C:\Users\yrred\Documents\New project 2`; this was later moved to the saved Tesseract project.
- Decision - The hourly sprite-sheet automation must use only one configured workspace, `C:\Users\yrred\Desktop\Obsidian\Tesseract`, because multiple `cwds` caused duplicate project/chat runs and invisible automation windows.
- Source: User report and automation review, 2026-05-12.

- Decision - The hourly sprite-sheet automation must acquire `.sprite-sheet-runner.lock.json` before queue selection and skip if another fresh lock exists.
- Source: User report and automation review, 2026-05-12.

- Decision - The recurring sprite-sheet automation is paused after `CHUNK_QUEUE.md` reached zero `Pending` rows and all `117` triad chunks were marked `QA Passed`.
- Source: [[short-term/2026-05-17-twb-creature-spritesheet-auto-ro-13]]

- Superseded - `CY-01` / `cybernetics` / `boreal_forest` was complete and marked `QA Passed`; the next recommended production chunk was `CY-02` / `cybernetics` / `desert`.
- Fact - `CY-02` / `cybernetics` / `desert`, `CY-03` / `cybernetics` / `freshwater`, `CY-04` / `cybernetics` / `grassland`, and `CY-05` / `cybernetics` / `industrial` are complete and marked `QA Passed`.
- Decision - The next recommended production chunk is `CY-06` / `cybernetics` / `marine`.
- Source: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-creature-spritesheet-auto-cy-01.md`

- Fact - `CY-08` / `cybernetics` / `rural_agricultural` is complete and marked `QA Passed` with `atk-needletag-rooster`, `def-gateplate-goat`, and `util-silochirp-swallow`.
- Fact - `CY-09` / `cybernetics` / `temperate_forest` is complete and marked `QA Passed` with `atk-lensjaw-fox`, `def-barkpatch-porcupine`, and `util-tripwire-wren`.
- Superseded - The next recommended production chunk was `CY-06` / `cybernetics` / `marine`; that gate has since passed.
- Superseded - The next recommended production chunk was `CY-10` / `cybernetics` / `tropical_forest`; that gate has since passed.
- Fact - `FA-02` / `faith` / `desert`, `FA-03` / `faith` / `freshwater`, `FA-04` / `faith` / `grassland`, and `FA-05` / `faith` / `industrial` are complete and marked `QA Passed`.
- Fact - `FA-10` / `faith` / `tropical_forest`, `FA-11` / `faith` / `tundra`, `FA-12` / `faith` / `urban_commercial`, and `FA-13` / `faith` / `urban_residential` are complete and marked `QA Passed`.
- Superseded - The next recommended production chunk was `FA-10` / `faith` / `tropical_forest`; that gate has since passed.
- Fact - `MA-01` / `magic` / `boreal_forest`, `MA-02` / `magic` / `desert`, and `MA-03` / `magic` / `freshwater` are complete and marked `QA Passed`.
- Superseded - The next recommended production chunk was `MA-01` / `magic` / `boreal_forest`; that gate has since passed.
- Fact - `MA-04` / `magic` / `grassland` is complete and marked `QA Passed` with `atk-shardbloom-thistlekin`, `def-wardstem-thistlekin`, and `util-sootpollen-thistlekin`.
- Fact - `MA-05` / `magic` / `industrial` is complete and marked `QA Passed` with `atk-sparkgnaw-tenrec`, `def-boilerback-roach`, and `util-chalkwing-moth`.
- Fact - `MA-06` / `magic` / `marine` is complete and marked `QA Passed` with `atk-sparkspine-shellkin`, `def-refractshell-shellkin`, and `util-wakeglow-shellkin`.
- Fact - `MA-07` / `magic` / `park` is complete and marked `QA Passed` with `atk-coinpeck-starling`, `def-markerback-toad`, and `util-ribbonmote-firefly`.
- Fact - `MA-08` / `magic` / `rural_agricultural` is complete and marked `QA Passed` with `atk-spurhex-rooster`, `def-baleback-toad`, and `util-cornsilk-caddisfly`.
- Fact - `MA-09` / `magic` / `temperate_forest` is complete and marked `QA Passed` with `atk-sparkclaw-cairnroot`, `def-wardback-cairnroot`, and `util-mosshush-cairnroot`.
- Fact - `MA-10` / `magic` / `tropical_forest` is complete and marked `QA Passed` with `atk-stormthread-spitter`, `def-basinweb-warder`, and `util-hushlace-dewspinner`.
- Fact - `MA-11` / `magic` / `tundra` is complete and marked `QA Passed` with `atk-splinterpika`, `def-cairnback-vole`, and `util-wickwhisk-lemming`.
- Superseded - The next recommended production chunk was `MA-08` / `magic` / `rural_agricultural`; that gate has since passed.
- Fact - `MA-12` / `magic` / `urban_commercial` and `MA-13` / `magic` / `urban_residential` are complete and marked `QA Passed`.
- Fact - `MI-01` / `might` / `boreal_forest` is complete and marked `QA Passed` with `atk-ripsnout`, `def-knotback`, and `util-mireturn`.
- Fact - `MI-02` / `might` / `desert` is complete and marked `QA Passed` with `atk-briartusk-boar`, `def-thatchback-bulwark`, and `util-quillwhistle-degu`.
- Superseded - The next recommended production chunk was `MA-12` / `magic` / `urban_commercial`; that gate has since passed.
- Fact - `MI-07` / `park`, `MI-08` / `rural_agricultural`, `MI-09` / `temperate_forest`, and `MI-10` / `tropical_forest` are complete and marked `QA Passed`.
- Superseded - The next recommended production chunk was `MI-03` / `might` / `freshwater`; that gate has since passed.
- Fact - `MI-11` / `might` / `tundra`, `MI-12` / `might` / `urban_commercial`, and `MI-13` / `might` / `urban_residential` are complete and marked `QA Passed`; Might affinity is complete through `MI-13`.
- Fact - `MN-01` / `mind` / `boreal_forest` is complete and marked `QA Passed`.
- Decision - The next recommended production chunk is `MN-02` / `mind` / `desert`.
- Fact - `RO-04` / `robotics` / `grassland`, `RO-05` / `robotics` / `industrial`, and `RO-06` / `robotics` / `marine` are complete and marked `QA Passed`.
- Fact - `RO-07` / `robotics` / `park` is blocked mid-triad: `atk-barbjaw-runner` and `def-postshell-grazer` are QA passed, while `util-thistlekite-relay` failed generation and the queue remains pending.
- Fact - `RO-10` / `robotics` / `tropical_forest` is complete and marked `QA Passed` with `atk-vinecutter`, `def-rootbrace`, and `util-signalmidge`.
- Superseded - The next recommended production chunk was `RO-07` / `robotics` / `park`; that gate remains blocked mid-triad.
- Superseded - The next recommended production chunk was `RO-11` / `robotics` / `tundra`; that gate has since passed and the queue is now complete.
- Superseded - The next recommended production chunk was `RO-04` / `robotics` / `grassland`; that gate has since passed.
- Warning - `FA-02` utility gecko prompts should explicitly call out front, side, and back rows after `util-coolveil-gecko` required a regeneration for row-order correction.
- Source: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-creature-spritesheet-auto-fa-02.md`
- Source: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-creature-spritesheet-auto-fa-03.md`
- Source: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-creature-spritesheet-auto-fa-04.md`
- Source: `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-14-twb-creature-spritesheet-auto-fa-05.md`

## Warnings

- Warning - The Unity repo may have many unrelated dirty changes. Future workers must avoid broad cleanup or revert operations.
- Warning - Mechanical QA does not prove motion quality; visual QA remains required.
- Warning - Generated source images under `.codex\generated_images\` may be useful provenance and should not be deleted without user instruction.
- Warning - Lime/green matte artifacts have appeared in generated walk sheets. Treat any visible chroma outline or cutout fringe as QA failure, even if mechanical alpha checks pass.
- Warning - Multiple configured workspaces for the same cron automation can create duplicate runs in different project windows and waste generation effort on the same folder.
- Warning - Lightweight utility creatures should be prompted explicitly so armor density does not drift toward heavier attack or defence silhouettes.
