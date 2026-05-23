# Marketing Report - 2026-05-11 - World Keys Pre-Live Deployment

## Task

Deploy the approved pre-live World Keys website funnel to production.

## Deployment Result

- Status: Deployed and live-verified.
- Production URL: `https://the-world-beneath.com/`
- Production version: `6a0ee9b8-c27c-4ed9-be6a-ddd38da54d55`
- Wrangler uploaded exactly two changed static assets:
  - `/index.html`
  - `/world-keys/index.html`

## Source Control

- Branch: `codex/world-keys-prelive-funnel-20260511`
- Commit: `2ec5a72` - `Update World Keys pre-live funnel`
- PR: `https://github.com/dodo-arcforge-interactive/the-world-beneath-site/pull/3`
- PR status: Merged
- Merge commit: `1e55a67`
- Local branch after merge: `main`
- Local status after merge: clean

## Live Verification

Homepage:

- URL: `https://the-world-beneath.com/`
- Status: `200`
- Title: `The World Beneath - The Garden and The Alchemy Lab Opening Soon`
- Confirmed live copy:
  - `The Garden and The Alchemy Lab are opening first.`
  - `Follow the World Keys`
  - `Read deeper into the story`

World Keys page:

- URL: `https://the-world-beneath.com/world-keys/`
- Status: `200`
- Title: `Free World Keys - The Garden and The Alchemy Lab | The World Beneath`
- Confirmed live copy:
  - `The Garden and The Alchemy Lab are the first doors.`
  - `Follow The Garden`
  - `Follow The Alchemy Lab`
- Confirmed removed old copy:
  - `No public World Key game is live right now.`

## Checks Run

- `git status --short --branch`
- `git diff --check`
- `git diff --stat`
- `npx wrangler deploy --dry-run`
- `npx wrangler deploy`
- `Invoke-WebRequest https://the-world-beneath.com/`
- `Invoke-WebRequest https://the-world-beneath.com/world-keys/`
- `gh pr checks 3 --watch --interval 10`
- `gh pr merge 3 --merge --delete-branch`

## Risks

- Risk - The site is now pre-live for World Keys, so it should not remain in this state once either key is actually playable.
- Risk - CTAs still point to `/world-keys/` and `/register/`, not itch.io, because itch.io pages are not confirmed.
- Risk - The Garden card uses existing artwork, not final dedicated World Key art.

## Memory-Worthy Notes

- Decision - Pre-live World Keys funnel is now live on production.
- Decision - Homepage and World Keys page should switch to play-now copy when The Garden or The Alchemy Lab has a real playable URL.
- Warning - Do not deploy play-now language until the player can actually play.

## Do Not Promote To Memory

- No itch.io URLs were confirmed.
- No World Key build readiness was confirmed.
- No Kickstarter page was created.
- No Steam page was created.

## Follow-Up Recommendations

1. Prepare itch.io release briefs and page copy for The Garden and The Alchemy Lab.
2. Confirm build readiness for the first public World Key.
3. Replace follow/register CTAs with play-now links when the first itch.io page is live.
4. Produce dedicated art/screenshots for each World Key before a larger campaign push.
