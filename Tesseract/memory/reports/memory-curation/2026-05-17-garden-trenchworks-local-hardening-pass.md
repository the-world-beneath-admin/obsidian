# Garden And Trenchworks Local Hardening Pass

Date: 2026-05-17

## Task

Implement the first Codex project-hardening gate for the active Garden and Trenchworks lanes.

## Result

Added local project entry docs for both active lanes. The Garden now has a real `npm run typecheck` script. Trenchworks now has local docs that distinguish solution build checks from Unity Play Mode checks.

## Files Touched

The Garden:

- `C:\Users\yrred\Desktop\Unity\TWB-Farming\AGENTS.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\architecture.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\testing.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\conventions.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\docs\common-pitfalls.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Farming\package.json`

TWB Trenchworks:

- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\AGENTS.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\docs\architecture.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\docs\testing.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\docs\conventions.md`
- `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks\docs\common-pitfalls.md`

Memory:

- `memory/wiki/game-dev/build-test-commands.md`
- `memory/wiki/memory/codex-project-hardening-standard.md`
- `memory/briefs/current-codex-project-hardening-task.md`
- `memory/hot.md`
- `memory/index.md`
- `memory/log.md`

## Checks Run

- `npm run typecheck` in `C:\Users\yrred\Desktop\Unity\TWB-Farming` - passed.
- `npm run build` in `C:\Users\yrred\Desktop\Unity\TWB-Farming` - passed with the existing Vite large chunk warning.
- `dotnet build TWB-TrenchWorks.sln --no-restore` in `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` - passed with 0 warnings and 0 errors.
- Verified no active memory/brief/prompt references still use the misspelled `Markeing` path.

## Memory-Worthy Notes

- The Garden now has local `AGENTS.md` and `docs/` entry docs plus a real `npm run typecheck` alias.
- TWB Trenchworks now has local `AGENTS.md` and `docs/` entry docs.
- Trenchworks command-line solution build passes, but Unity Play Mode remains a separate required check for scene, rendering, input, and runtime visual work.
- Neither `C:\Users\yrred\Desktop\Unity\TWB-Farming` nor `C:\Users\yrred\Desktop\Unity\TWB-Trenchworks\TWB-TrenchWorks` appears to be a git repository from its own folder.

## Remaining Gaps

- The Garden still has no real lint or test script.
- Trenchworks still needs a stable command-line Unity automation wrapper if recurring non-interactive Play Mode verification becomes important.
- TWB-Marketing, The Alchemy Lab, the main Unity project, and the website/shared platform still need their own local hardening pass.

## Next Recommended Gate

Resume feature work in The Garden or Trenchworks using the new local docs. Next hardening pass should target TWB-Marketing and the website/shared platform, since both already have useful command surfaces and would benefit from local `docs/` entry pages.
