# Current Marketing Task

## Status

Active - website realignment plan for Garden release, Trenchworks introduction, main-game repositioning, forum updates, creator/community framing, and Kickstarter runway.

## Workflow

- [[wiki/marketing/seo-research-workflow]]
- [[wiki/launch/kickstarter-phase-one-strategy]]
- [[wiki/launch/kickstarter-readiness-board]]

## Goal

Update `the-world-beneath.com` so it reflects the current project truth:

- The World Beneath is a playable living-world project, not only a book or one distant main game.
- The Garden is the first World Key and first public playable proof.
- TWB Trenchworks is the next standalone TWB-tagged Unity game coming down the pipe.
- The main game remains the parent/shared-world RPG spine.
- Forum updates replace the old standalone Progress/Roadmap page.
- Creator/community participation is a visible pillar, with legally cautious wording.

## Scope

Website/shared platform public marketing work:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

Project scope category:

- Shared platform/account system
- Main game / The World Beneath positioning
- Glassroot Garden World Key launch positioning
- Standalone TWB-tagged game positioning for Trenchworks
- Kickstarter launch preparation

## Read First

- [[hot]]
- [[index]]
- [[wiki/game-dev/project-hierarchy]]
- [[wiki/launch/kickstarter-phase-one-strategy]]
- [[wiki/launch/kickstarter-readiness-board]]
- [[wiki/marketing/founding-creator-outreach-package]]
- [[wiki/shared-platform/creator-commercial-license-structure]]
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\AGENTS.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\README.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\architecture.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\testing.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\conventions.md`
- `C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site\docs\common-pitfalls.md`

## Likely Website Touch Points

- `index.html`
- `world-keys\index.html`
- new Garden landing route, likely `world-keys\the-garden\index.html` or `garden\index.html`
- new `trenchworks\index.html`
- `game\index.html`
- `progress\index.html` or Worker redirect handling
- `community\index.html`
- `creator-call\index.html` if Bob approves publishing it
- `assets\js\site.js`
- `assets\js\config.js` only if launch/play/Kickstarter links are added
- `assets\css\styles.css` and any page CSS needed
- `sitemap.xml`
- `worker.js` only if route redirects are implemented there

## Positioning Decisions For This Pass

- Lead with the current shape: playable World Keys, main RPG spine, Trenchworks, shared account/community, creator participation, and Kickstarter runway.
- Treat The Garden as first playable proof. Use absolute date wording only after Bob confirms final release timing and play URL.
- Treat Trenchworks as active prototype / next TWB-tagged game, not finished reward software until its reward proof gate is closed.
- Treat the main game as the long-term parent RPG and systems spine, not as the only product.
- Retire `/progress/` from nav/footer and CTAs, but preserve the route as a redirect or "updates moved to forum" page rather than hard-deleting it.
- Keep book/audiobook as lore foundation, lower than playable projects on the public funnel.
- Keep creator-platform and commercial-license wording non-final until Bob approval plus legal/accounting review.

## Constraints

- Do not imply the full main game is playable now.
- Do not promise account sync/import/carryover beyond what exists.
- Do not claim Trenchworks Steam delivery is guaranteed; keep fallback wording if delivery is discussed.
- Do not publish final creator-license terms, revenue/royalty claims, investment language, equity, backer returns, or canon approval promises.
- Do not deploy the website without explicit approval.
- Do not run remote D1 migrations without explicit approval.
- Do not update permanent `memory/wiki/`, `memory/index.md`, `memory/hot.md`, or `memory/log.md` from a worker window.

## Verification Path

Run from:

```powershell
cd C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

Preferred local checks:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1 -SkipWranglerDryRun
node --check .\assets\js\site.js
node --check .\worker.js
```

Before deployment discussion:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1
npx wrangler deploy --dry-run
```

Remote deploy remains blocked until Bob explicitly approves.

## Done Criteria

- Site architecture plan exists and has Bob/orchestrator review.
- Homepage plan makes the new project shape obvious in the first viewport.
- World Keys page plan elevates The Garden and clarifies Alchemy as a future World Key.
- Dedicated Garden page plan exists for launch/play CTA, controls, account/pet relationship, screenshots, support, and known issues.
- Dedicated Trenchworks page plan exists and accurately explains the factory/logistics plus automated trench-war concept.
- Main Game page plan explains the parent RPG and current systems without making it sound like the first public release.
- Progress/Roadmap retirement plan removes nav/footer/CTA links and routes updates to the forum.
- Creator/community wording is cautious and Kickstarter-safe.
- Worker handoff defines allowed paths, forbidden paths, checks, and report destination.
- Report written to `memory/short-term/`.

## Report Required

Write to:

```text
C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\YYYY-MM-DD-website-project-realignment-plan.md
```

Include:

1. Scope
2. Current-site findings
3. Recommended site architecture
4. Page-by-page plan
5. Copy/claim constraints
6. Open decisions for Bob
7. Worker handoff
8. Verification plan
