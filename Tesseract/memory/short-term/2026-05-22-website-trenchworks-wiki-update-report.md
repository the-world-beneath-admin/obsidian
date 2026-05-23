# Website Trenchworks Wiki Update Report

Date: 2026-05-22

## Scope

Shared website / local website wiki for The World Beneath and TWB Trenchworks.

## What Changed

- Added a two-choice wiki selector on `/wiki/`:
  - `The World Beneath: Main`
  - `The World Beneath: Trenchworks`
- Added header and footer wiki sub-links so Main and Trenchworks stay separated.
- Extended the wiki generator and front-end reader to support a `Wiki` metadata field.
- Added image rendering support inside wiki markdown.
- Added Trenchworks website assets copied from the current Unity project:
  - 33 soldier role images
  - MG nest review images
  - rifleman emplacement review images
  - General portrait
  - Mysterious Factory Coordinator portrait
- Regenerated the website wiki JSON bundles.

## New Main Wiki Entry

- `Trenchworks`
  - Source: `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\WikiSystem\pages\CanonWiki\World_Beneath\Trenchworks.md`
  - Purpose: basic bridge blurb from the main TWB wiki into the separate Trenchworks wiki.

## New Trenchworks Wiki Entries

- `TWB Trenchworks`
- `Trenchworks Soldier Art`
- `MG Emplacement Art`
- `Rifle Emplacement Art`
- `MG Nest`
- `Rifleman Emplacement`
- `The General`
- `Mysterious Factory Coordinator`

Source folder:

`C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Documentation\WikiSystem\pages\CanonWiki\Trenchworks`

## Website Files Touched

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\scripts\build-wiki-data.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\wiki.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\site.js`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\styles.css`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\wiki\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\data\wiki\public.json`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\data\wiki\supporter.json`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\data\wiki\creator.json`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\data\wiki\manifest.json`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\images\trenchworks\`

## Checks Run

- `node .\scripts\build-wiki-data.js`
- `node --check .\assets\js\wiki.js`
- `node --check .\scripts\build-wiki-data.js`
- `node --check .\assets\js\site.js`
- `powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1`
- Local browser smoke:
  - `/wiki/?wiki=trenchworks` loads with Trenchworks selector active.
  - Soldier art page renders 33 images.
  - Main wiki Trenchworks bridge page loads under Main.
  - Header submenu exposes Main and Trenchworks wiki links.

## Cleanup Performed

- Stopped the temporary local Python preview server on port `8007`.
- No live deployment was performed.
- No remote migrations were run.
- No staging, commit, reset, or broad cleanup was performed.

## Risks

- The website repository already had many unrelated dirty files before/around this pass; deploy review must separate these wiki changes from existing work.
- The Trenchworks wiki source pages currently live under the main Unity wiki source tree because that is the existing source consumed by the website generator.
- The soldier art page intentionally references role art, not every deployable squad template. Squad templates remain a separate implementation/design catalog.

## Memory-Worthy Notes

- The live/local website wiki now supports separate wiki identities using page metadata.
- TWB Trenchworks has a separate website wiki surface from the main World Beneath wiki.
- Manned emplacement and unit-art pages now have public-facing local wiki entries for the current prototype art set.

## Follow-Up Recommendations

1. Review the local wiki visually with Bob before live deployment.
2. If approved, deploy the website with explicit approval only.
3. Later, add deeper pages for all 50 deployable squads once the command-system implementation packet is approved.
