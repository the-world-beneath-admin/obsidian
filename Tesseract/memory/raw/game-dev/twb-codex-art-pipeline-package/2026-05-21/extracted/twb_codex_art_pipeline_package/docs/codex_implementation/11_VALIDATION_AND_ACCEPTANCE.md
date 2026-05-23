# Validation and Acceptance

## Purpose

Codex must validate the work before calling it done.

## Compile validation

Check that:

- all scripts compile
- no missing namespaces
- no editor-only code in runtime assemblies
- no runtime scripts inside Editor folders unless intended
- no references to missing packages
- no missing prefab scripts

## Asset validation

Check that:

- generated PNGs exist
- sprites import as sprites
- transparent assets have alpha
- prefabs reference valid sprites
- animation scripts reference valid frame arrays
- VFX prefabs have frame sequences
- generated reports exist

## Scene validation

Open or inspect:

```text
Assets/TWB/Scenes/TWB_ArtPipeline_VerticalSlice.unity
```

Check that:

- camera exists
- objects are visible
- sprites have correct sorting
- scene root is organized
- at least one animated unit exists
- VFX objects exist
- UI markers exist
- no missing script warnings
- no missing sprite references

## Visual acceptance checklist

The vertical slice is acceptable if:

- trench reads clearly
- sandbag walls read clearly
- MG is identifiable
- mortar is identifiable
- infantry look like helmeted soldiers with guns
- vehicle is identifiable
- props add battlefield/logistics context
- VFX sells weapon activity
- UI markers are not raw debug shapes
- palette is consistent
- the scene looks complete enough for a prototype

## Report requirement

Create:

```text
Assets/TWB/Docs/ART_PIPELINE_IMPLEMENTATION_REPORT.md
```

Report must include:

1. summary of what was implemented
2. generated folder structure
3. list of generated art assets
4. list of prefabs
5. list of scripts
6. scene path
7. how to regenerate art
8. how to use prefabs
9. known limitations
10. next recommended tasks

## Known limitations honesty

If something could not be completed, document it directly.

Do not hide failures.

Examples:

- “Sprite sheet slicing was skipped; individual frame files were generated instead.”
- “Tilemap integration was not added because project uses custom terrain.”
- “VFX are prototype quality but functional.”
- “Animation clips are represented with simple runtime sprite arrays.”

## Final acceptance language

The final report should end with:

```text
Prototype art pipeline status: usable first pass.
Recommended next step: connect generated prefabs to real gameplay systems.
```
