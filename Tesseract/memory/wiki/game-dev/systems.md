# Systems

## Summary

Scope: World Key: Glassroot Garden.

The current game systems are farming automation, crop growth, optional timed work, harvesting, raw/dried storage, drying, recipe-based bundling, finished bundle timers, Notice Board contracts, World Key shared storage, progression, and future account/platform persistence.

## Memory Items

- Fact - Required farming work is automated by Companions: till soil, fetch seed, plant crop, and harvest ready crop.
- Fact - Optional crop work windows are player-timed. Clicking during an open window queues Companion work that may add yield bonus or penalty.
- Fact - Plot states include `untilled`, `tilling`, `tilled`, `planting`, `growing`, `ready`, and `harvesting`.
- Fact - Raw plant bins and dried plant bins each use slotted storage with caps. Overflow can route to compost in the planned storage model.
- Fact - The bundler requires the selected recipe's dried plants in order before it can create a finished bundle.
- Fact - Finished bundles can resolve into Notice Board rewards or World Key shared storage.
- Hypothesis - Processing, contracts, XP, and storage are the first major expansion lane after the core farm loop because they make harvest outputs meaningful.
- Source: [[memory/raw/game-design/glassroot/Magitech_Farming_Work_Stages_Implementation_Plan]]
- Source: [[memory/raw/game-design/glassroot/Next_Phase_Magitech_Processing_And_Contracts_Plan]]
- Source: [[memory/raw/game-design/glassroot/Full_Loop_Test_And_Implementation_Plan]]
