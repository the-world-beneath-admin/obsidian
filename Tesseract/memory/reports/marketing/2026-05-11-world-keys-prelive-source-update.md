# Marketing Report - 2026-05-11 - World Keys Pre-Live Source Update

## Task

Apply the approved pre-live World Keys funnel copy to the local website source.

## Branch

`codex/world-keys-prelive-funnel-20260511`

## Pages Changed

- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\index.html`
- `C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site\world-keys\index.html`

## Copy Changes

- Homepage now leads with The Garden and The Alchemy Lab opening first.
- Homepage uses pre-live language:
  - "being prepared"
  - "opening first"
  - "Follow the World Keys"
- Homepage moves book/audiobook language into a deeper story path.
- Homepage adds a "Start with a World Key" section with cards for The Garden, The Alchemy Lab, and the full game.
- World Keys page now names The Garden and The Alchemy Lab as the first two free World Keys.
- World Keys page replaces "no public World Key game is live right now" / "replacement first key" language with pre-live release status language.
- World Keys page explains what World Keys are and how they connect to the full game.

## Visual/Layout Changes

- No new CSS files were created.
- Existing card, hero, and World Keys page structures were reused.
- The Garden and The Alchemy Lab cards now appear as the first release focus.
- A decorative media image was added to The Garden card so the two World Key cards balance visually.

## Checks Run

- `git status --short --branch`
- `npx wrangler deploy --dry-run`
- Served local preview at `http://127.0.0.1:8002/`
- Playwright opened and snapshotted:
  - `http://127.0.0.1:8002/`
  - `http://127.0.0.1:8002/world-keys/`
- Playwright screenshots checked visually for desktop and mobile layouts.
- Removed generated `.playwright-cli` artifacts before final dry-run so they would not be included as deployable assets.
- Final Wrangler dry-run read `2592` files and passed.

## Preview Notes

- Static local preview showed `/api/me` 404 console errors because the Python static server does not run the Worker API.
- Homepage also showed a ConvertKit network error in static preview. This appears environment/network related and not caused by the copy change.
- No deployment was performed.

## Risks

- Risk - The pre-live copy still needs user visual approval before deployment.
- Risk - CTAs currently point to `/world-keys/` and `/register/`, not itch.io, because itch.io URLs are not confirmed.
- Risk - When either key becomes playable, copy should be switched from pre-live to play-now.
- Risk - The Garden card image is a reused existing world image, not final dedicated World Key art.

## Memory-Worthy Notes

- Decision - Use pre-live website copy until The Garden or The Alchemy Lab has a real playable link.
- Decision - Do not deploy this branch without explicit user approval.
- Warning - Keep generated Playwright artifacts out of the deployable website asset tree.

## Do Not Promote To Memory

- No launch date was chosen.
- No itch.io URL was confirmed.
- No final World Key art was approved.
- No deployment was performed.

## Follow-Up Recommendations

1. User reviews the local preview.
2. If approved, commit and open a PR or prepare deployment.
3. Deploy only after explicit deployment approval.
4. When itch.io pages are live, switch to play-now copy and direct CTAs.
