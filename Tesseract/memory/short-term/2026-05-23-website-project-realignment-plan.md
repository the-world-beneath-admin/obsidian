# Website Project Realignment Plan

Date: 2026-05-23

## Scope

Lane: website/shared platform marketing, launch preparation, and public project positioning.

Website source:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

Goal: realign `the-world-beneath.com` before Garden release and Kickstarter preparation so the site no longer presents The World Beneath as only a book or one distant main game. The public funnel should show a living project with playable World Keys, the main RPG spine, standalone TWB-tagged games, shared account/community systems, and a creator path.

This is planning only. No website source was changed in this pass.

## Context Read

- `memory/hot.md`
- `memory/index.md`
- `memory/wiki/game-dev/project-hierarchy.md`
- `memory/wiki/launch/kickstarter-phase-one-strategy.md`
- `memory/wiki/launch/kickstarter-readiness-board.md`
- `memory/wiki/marketing/founding-creator-outreach-package.md`
- `memory/wiki/shared-platform/creator-commercial-license-structure.md`
- website `AGENTS.md`
- website `README.md`
- website `index.html`
- website `world-keys/index.html`
- website `game/index.html`
- website `progress/index.html`
- website `assets/js/site.js`
- website `sitemap.xml`
- website `creator-call/index.html`
- website `worker.js`

## Current-Site Findings

- The homepage still leads with "The Garden and The Alchemy Lab are opening first." That is closer than the old book-only site, but it does not explain the larger current project: Garden, Trenchworks, main game, shared platform, creators, forum updates, and Kickstarter runway.
- `/world-keys/` still frames both The Garden and The Alchemy Lab as "being prepared." It does not yet present The Garden as the first imminent playable proof.
- There is no dedicated public Garden launch page under `world-keys/` or `/garden/`.
- There is no dedicated Trenchworks page, only a wiki selector link.
- `/game/` describes the shared-world RPG well, but still links visitors to `/progress/` and does not explain how the main game now sits beside World Keys and Trenchworks.
- `/progress/` is still a full roadmap page, and `assets/js/site.js` includes Progress in the top nav, footer, footer-bottom, and some CTAs.
- `sitemap.xml` still lists `/progress/`.
- `/creator-call/` exists but is `noindex` and not surfaced in nav/footer. Its caution language is good; publishing it needs Bob approval.
- The site has existing support-ticket entry points and admin platform work, so public pages should point users to the forum/support path rather than inventing a second feedback mechanism.

## Planning Lens

The `twb-planning` triad was simulated inline because this orchestration window is producing a plan, not launching execution children.

Helpful Genius:

- Make the homepage a project map: The Garden now, Trenchworks next, main game as the spine, creators/community as the growth engine.
- Use The Garden as proof-of-world and route visitors to play/follow/report.
- Give Trenchworks its own page so Kickstarter visitors can understand the first paid/reward candidate.

Devil's Advocate:

- Do not overpromise. The Garden can be "first playable proof" only once the play URL/build is real. Trenchworks is not reward-ready until visual/prototype proof is packaged.
- Do not hard-delete `/progress/`; old links and search results should land on a moved-updates page or redirect.
- Do not publish commercial-license percentages or creator promises as final legal language.

Doe-Eyed Intern:

- A new visitor needs answers in seconds: What can I play? What is a World Key? What is Trenchworks? Is the book still relevant? Where are updates? How can I join or create?

## Master Site Architecture

### Homepage `/`

Purpose: first-viewport explanation of the current project.

Recommended hero message:

```text
The World Beneath is a game world growing in public.
```

Support copy direction:

- A playable first World Key opens with The Garden.
- The main game is the long-term shared-world RPG spine.
- Trenchworks is the next TWB-tagged standalone game.
- The community, forum, account system, creator path, book, and audiobook all feed one living world.

Homepage sections:

1. Hero: living-world project, Garden CTA, forum/Discord/account CTA.
2. "Play first": The Garden card with launch status and play/follow CTA.
3. "Coming next": Trenchworks card with concise concept and status.
4. "The main game": parent RPG systems overview using real system screenshots where available.
5. "Creators and community": forum updates, creator call, creator policy, Discord, support.
6. "Lore foundation": book/audiobook moved lower, not removed.

### World Keys `/world-keys/`

Purpose: explain World Keys as focused playable doors into TWB.

Changes:

- Elevate The Garden as first World Key / first public playable proof.
- Move The Alchemy Lab to "future World Key" or "next World Key candidate" unless Bob wants it still equal-billed.
- Explain shared account/pets carefully: website account is root identity; pets can be shared account companions where implemented; materials remain game-local unless exported by a supported system.
- Add route to the Garden page.

### Garden Page `/world-keys/the-garden/` or `/garden/`

Purpose: launch page for the first release.

Recommended route: `/world-keys/the-garden/` for hierarchy clarity, with optional `/garden/` redirect later.

Page contents:

- Title: `The Garden - First World Key`
- Play CTA once final URL exists.
- Release status with exact date if Bob confirms: 2026-05-24.
- Short loop: choose starter pets, tend plants, process materials, complete notice-board orders, gather progress.
- Account note: create/login through the website; do not promise unsupported sync.
- Starter pet note: pets are account-linked companions; Garden uses its own World Key subskill/progression where supported.
- Controls/help/known issues.
- Screenshots/GIFs from the accepted build.
- Support ticket/report bug CTA.
- Forum update CTA.

### Trenchworks Page `/trenchworks/`

Purpose: make the next project understandable before Kickstarter.

Public concept:

```text
TWB Trenchworks is a standalone Unity 2D factory/logistics game under The World Beneath banner. Players build the supply chain; automated old-school game AI armies use those supplies to dig, hold, and destroy their way across a trench-war battlefield.
```

Page sections:

1. What it is: factory/logistics + automated trench war.
2. How the player plays: harvest, refine, manufacture, ship inputs.
3. How the war plays out: two factions dig, fight, trench, surface/underground layers, eventual base destruction.
4. Why it belongs in TWB: another lens into the same world and creator/community platform.
5. Current state: active Unity prototype / controlled systems test; not final reward build.
6. Kickstarter relevance: candidate first paid digital game reward, with delivery wording blocked until proof package and platform choice are final.
7. Follow updates on the forum.

### Main Game `/game/`

Purpose: reposition as the parent RPG and long-term systems spine.

Changes:

- Rename conceptual framing from just "Game" to "The World Beneath - Main Game."
- Explain it is not being abandoned; it is the larger RPG that World Keys and standalone games orbit.
- Show systems already designed/prototyped:
  - dungeon/reward flow
  - inventory/archive/card surfaces
  - crafting and apply flows
  - starter pets/account companion path
  - world map and territory layer
  - HoloGlyph UI direction
- Remove `/progress/` CTAs.
- Replace roadmap CTA with forum updates and Kickstarter/newsletter CTA.
- Use main-game screenshots from the Kickstarter raw capture set after asset selection/copy into the website is approved.

### Progress/Roadmap `/progress/`

Purpose: retire without breaking visitors.

Recommendation:

- Remove Progress from nav/footer and all active CTAs.
- Keep `/progress/` as a short moved page or Worker redirect.
- Best first implementation: keep a static page that says development updates now live in the forum, with links to:
  - `/community/forum/`
  - `/game/`
  - `/world-keys/`
  - `/trenchworks/`
- Then remove `/progress/` from sitemap after confirming no active CTA depends on it.

### Community And Forum

Purpose: become the update center.

Recommended public board framing:

- Development Updates
- The Garden
- Trenchworks
- Main Game
- Creator Workshop
- Support / Bug Reports

If forum categories are database-seeded rather than static, do not change them in the website-copy pass without checking migrations/API seed flow.

### Creator Path

Purpose: show that TWB is becoming a creator-grown world without making unsafe legal promises.

Options:

1. Conservative: leave `/creator-call/` noindex and link only from the forum/Discord/Kickstarter draft until Bob approves.
2. Public: remove `noindex`, add "Creators" to footer/nav, and link to creator policy.

Safe wording:

```text
The creator platform is planned to support selected creators with tools, guidelines, and review paths. Commercial licensing is not open yet and final terms will be published before creators are asked to rely on them.
```

Avoid:

- partner
- official canon creator
- guaranteed income
- investment opportunity
- revenue share for backers
- unlimited commercial license
- final royalty promises

## Implementation Gates

### Gate 1 - Copy And Route Plan

Deliverables:

- final page map
- Bob-approved public claims
- Garden play URL decision
- Trenchworks status wording
- progress retirement decision
- creator-call publish/noindex decision

### Gate 2 - Local Website Update

Worker edits:

- `index.html`
- `world-keys/index.html`
- `game/index.html`
- `progress/index.html`
- new Garden page
- new Trenchworks page
- `assets/js/site.js`
- `sitemap.xml`
- CSS only as needed
- `worker.js` only if redirect handling is chosen

### Gate 3 - Local Verification

Run:

```powershell
cd C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -SkipWranglerDryRun
node --check .\assets\js\site.js
node --check .\worker.js
```

Preview locally and screenshot at desktop and mobile widths.

### Gate 4 - Bob Review

Bob reviews:

- homepage first viewport
- Garden release claims and CTA
- Trenchworks page status
- main-game framing
- creator/legal caution
- progress route behavior

### Gate 5 - Deployment Prep

Only after Bob approval:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1
npx wrangler deploy --dry-run
```

Live deploy remains blocked until explicit approval.

## Worker Handoff

Scope:

- Website/shared platform public marketing realignment for The World Beneath.

Read first:

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\briefs\current-marketing-task.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\game-dev\project-hierarchy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\launch\kickstarter-phase-one-strategy.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\launch\kickstarter-readiness-board.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\AGENTS.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\architecture.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\testing.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\conventions.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\common-pitfalls.md`

Allowed write paths:

- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\index.html`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\world-keys\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\game\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\progress\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\trenchworks\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\js\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\assets\css\`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\sitemap.xml`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\worker.js` only if redirect is needed
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

Forbidden write paths:

- `memory/wiki/`
- `memory/index.md`
- `memory/hot.md`
- `memory/log.md`
- Unity game projects
- remote D1 migrations
- Cloudflare secrets
- live deployment
- legal terms finalization
- broad cleanup, reset, staging, or commits unless explicitly requested

Done criteria:

- Garden, Trenchworks, main game, World Keys, and homepage public positioning updated locally.
- Progress/Roadmap removed from nav/footer/CTAs and converted to moved-updates behavior.
- Forum is the clear update destination.
- Creator language is cautious and not final legal/commercial language.
- Local checks pass.
- Report written under `memory/short-term/`.

Report destination:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-website-project-realignment-implementation-report.md
```

## Open Decisions For Bob

1. Exact Garden play URL: hosted on `the-world-beneath.com`, itch.io, or both?
2. Can the site publicly say "The Garden opens May 24, 2026," or should it say "opening next" until the build/link is locked?
3. Should `/creator-call/` go public now, stay noindex, or wait until Kickstarter page drafting?
4. Should Trenchworks be top-level nav, footer-only, or under a "Projects" dropdown?
5. Should `/progress/` redirect immediately to `/community/forum/`, or stay as a moved-updates landing page for a while?
6. Should Alchemy remain equal-billed with Garden on the homepage, or move lower as a future World Key?
7. Which main-game screenshots from the Kickstarter capture set are approved for public website use?

## Recommended Next Gate

Approve Gate 1 decisions, then commission a website worker to implement the local copy/route update without deploying.
