# Live Site Baseline Check - 2026-05-11

## Task

Check the existing public website after the local homepage file was opened directly from disk and appeared as an unstyled black-and-white page.

## Result

The public website at `https://the-world-beneath.com/` is a full styled website with imagery, navigation, calls to action, and multiple project pages.

The black-and-white local preview was caused by opening `index.html` through `file://`. The site uses root-relative asset paths such as `/assets/css/styles.css`, which are correct for the live site or a local server, but unreliable when the file is opened directly from disk.

## Live Pages Checked

- `https://the-world-beneath.com/`
- `https://the-world-beneath.com/game/`
- `https://the-world-beneath.com/progress/`
- `https://the-world-beneath.com/world-keys/`

## Checks Run

- Opened the live homepage in the browser.
- Confirmed the live homepage has its full visual styling and assets.
- Checked homepage browser warnings/errors; none were reported during the quick check.
- Checked live text structure for Home, Game, Progress, and World Keys pages.
- Started a local static preview at `http://127.0.0.1:8000/`.
- Confirmed the local homepage source renders with full styling when served through HTTP.
- Checked served-preview browser warnings/errors; none were reported during the quick check.

## Risks

- Do not judge website visuals by opening local HTML files directly through `file://`.
- Do not deploy the current website folder blindly because the repo already contains unrelated local changes.
- Any homepage copy changes should be previewed through a local server or deployment preview before publishing.

## Memory-Worthy Notes

- Warning: website visual QA must use the live domain, a deployment preview, or a local web server. Direct `file://` previews can break root-relative CSS, JavaScript, and image paths.
- Fact: The World Beneath already has a public full website with Home, Game, Progress, and World Keys pages.
- Fact: The approved Variant 1 homepage copy renders correctly with full styling when served locally at `http://127.0.0.1:8000/`.
- Decision candidate: prepare a clean deployment plan before publishing approved copy changes.

## Follow-Up Recommendations

1. Create a clean deployment plan that isolates approved copy changes from unrelated dirty repository changes.
2. Preview local changes through a local static server or deployment preview.
3. Update Game page copy only after the deployment path is clean.
