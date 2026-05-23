# TWB Unity Worker Report - 2026-05-12 - SystemConsole Fail Cleanup

## Task

Main game / The World Beneath Unity project. Clear the pasted TWB SystemConsole fail list covering Card Summary, starter guardian catalog/biome validation, Home Defense, template determinism, and world-map zoom/tile-source contracts.

## Result

All 13 pasted failures now pass individually and also show `Pass` inside the broader full SystemConsole report.

The full SystemConsole run is not clean: `823/845` passed and `22` failed. The remaining failures are older world-map production/styled-tile/tooling guardrails, mostly expecting retired styled/no-label packs, missing `tools/worldmap` artifacts, or broader ops-table/styled-lane migration work. They were not in the pasted fail list and were not expanded into a broad world-map pipeline cleanup.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\CardSummarySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\WorldMapSurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\CardSummaryActionStripLayoutTest.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\CreatureCatalog\CreatureCatalogRegistryOrderingTest.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\CreatureDefinitions_RequireValidSingleBiomeTag_Test.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\HomeDefenseActivityTests.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\Templates\TemplateResolutionDeterminismTest.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\Editor\SystemConsole\Tests\WorldMapActivityTests.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 2 existing CS0649 warnings.
- `test-systemconsole -TestFilter card_summary` passed.
- `test-systemconsole -TestFilter creature_catalog_registry_ordering` passed.
- `test-systemconsole -TestFilter creature_definitions_require_valid_single_biome_tag` passed.
- `test-systemconsole -TestFilter home_defense_process_threat_and_rewards` passed.
- `test-systemconsole -TestFilter template_resolution_determinism` passed.
- `test-systemconsole -TestFilter world_map_live_tile_source_contract` passed.
- `test-systemconsole -TestFilter world_map_live_tile_request_projection` passed.
- `test-systemconsole -TestFilter world_map_global_zoom_table` passed.
- `test-systemconsole -TestFilter world_map_global_zoom_ui_projection_stable` passed.
- `test-systemconsole -TestFilter world_map_dungeon_traces_close_zoom_only` passed.
- Full `test-systemconsole` produced `823/845` passed, `22` failed; all 13 pasted failures were `Pass` in that report.
- `unity-automation.ps1 -Mode compile` loaded assemblies with no C# compile errors, but the wrapper marked failed because of the recurring Mono `abort_threads` error signal.

## Cleanup performed

No generated source/content cleanup was performed. Unity automation artifacts were preserved as evidence under `artifacts\unity-automation\`. Tracked files touched by patching were normalized back to CRLF line endings to avoid accidental line-ending churn.

## Risks

The repo was already heavily dirty, including untracked world-map and SystemConsole files. No broad cleanup, revert, staging, or commit was performed.

The remaining 22 full-console failures are clustered around old world-map styled/no-label production pipeline expectations and missing tool manifests/scripts. Fixing those cleanly should be a separate Bob-approved pass, not a quiet side quest.

Unity automation continues to report non-test error signals such as `RenderTexture.Create failed` in some UI test runs and `abort_threads` during compile. The named tests passed despite those wrapper signals.

## Memory-worthy notes

Peggy and Stanly should remain special starter guardian exceptions to regular biome tag validation; do not add `special_ephemrial_spirit` to the global biome registry just to satisfy regular creature validators.

Current world-map source/zoom contract in the touched tests is the ops-table tile lane with local/hosted sources, map zoom modes `5/6/8`, town tile projection at z8, and an 81-tile ops-table overscan budget.

Card Summary now has the intended top bar/action strip split: back, salvage, and confirm live under `CardSummary_ActionStrip`; the top bar holds the title; modifier scroll controls exist.

## Do not promote to memory

Do not promote this report wholesale. Review and promote only durable decisions after Bob/orchestrator confirms the ops-table world-map contract and the special-starter biome-validation exception.

## Next recommended gate

Run a dedicated world-map guardrail triage pass for the 22 remaining full-console failures. Decide whether each old styled/no-label/tile-tooling test should be migrated to the ops-table contract, restored with missing tooling artifacts, or retired as superseded.
