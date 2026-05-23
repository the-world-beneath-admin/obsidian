# TWB Unity Worker Report - 2026-05-15 - Pet Card Icons

## Task

Wire pet icon images into the main game card surfaces, starting with the special starter pets and covering the existing standard pet icon set. Scope was Main game / The World Beneath.

## Result

Added a Unity-side pet card icon resolver and bound it into Archive card tiles, Card Summary hero art, and dungeon party slot visuals. Special starter pets resolve through `StarterPetCatalog` key art/icon paths first. Standard T1 pet cards resolve through `PetCardIdentityAuthority` and the imported `Resources/GameArt/TWB_HoloGlyph_T1/PetIcons` icon set.

The old text placeholders remain as fallbacks only when no sprite is resolved.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-game-dev-task.md`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\TWB.UnityBridge.csproj`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\PetCardIconResourceResolver.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\PetCardIconUiBinding.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\UIShellBootstrap.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\CardSummarySurfaceBuilder.cs`
- `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Assets\_TWB\Scripts\UnityBridge\UI\Builders\DungeonSurfaceBuilder.cs`

## Checks run

- `dotnet build TWB_Phase1_IdlePrototype.sln --no-restore` passed with 0 errors and 2 pre-existing style/unused warnings.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode status` reported `probably-clean`, 0 error signals, 0 warning signals.
- `powershell -ExecutionPolicy Bypass -File .\tools\unity-automation.ps1 -Mode compile` was attempted. The automation returned `UnityExitCode: 0`, but the log reported batchmode aborted because this project was already open in another Unity instance, so this should not be treated as a full closed-editor batch compile.
- Asset spot checks found 351 standard pet icon PNGs under `Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons` and 12 special Ephemrial Spirit starter icon/key-art PNGs under `Assets\Resources\GameArt\TWB_HoloGlyph_T1\PetIcons\Special\EphemrialSpirit`.

## Cleanup performed

No temporary files were created for this slice. No broad cleanup or unrelated revert was performed.

## Risks

Unity may need to import the two new `.cs` files and generate `.meta` files in the open editor session before the live UI shows the new sprite children. The resolver depends on the imported PNGs being configured as sprites under `Resources`.

The `.csproj` uses explicit compile includes, so the new helper files were added there for `dotnet build`; future Unity project regeneration could reorder or refresh that file.

## Memory-worthy notes

Pet card icon lookup now has a single UI resolver path:

- Special starters: `StarterPetCatalog` `KeyArtResourcePath`, then `SpriteResourcePath`.
- Standard pets: card item id to creature id via `PetCardIdentityAuthority`, then filename slug lookup in `GameArt/TWB_HoloGlyph_T1/PetIcons`.

## Do not promote to memory

Do not promote this report directly. Bob/orchestrator should distill only the durable implementation fact if needed.

## Next recommended gate

Open Archive in the Unity editor with the linked online inventory and confirm the starter pet cards render their special icons/key art. Then inspect Card Summary and dungeon party slot selection for the same cards.
