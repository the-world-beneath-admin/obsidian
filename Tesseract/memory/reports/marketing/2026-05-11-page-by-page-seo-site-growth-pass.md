# Page-by-Page SEO Site Growth Pass - 2026-05-11

## Task

Run a focused SEO and site-growth pass from the merged website baseline.

Working branch:

```text
codex/seo-site-growth-pass-20260511
```

Local commit:

```text
1bb5dd8 - feat: improve page-level SEO signals
```

GitHub PR:

```text
PR: https://github.com/dodo-arcforge-interactive/the-world-beneath-site/pull/2
State: Merged
Base: main
Head: codex/seo-site-growth-pass-20260511
Merge commit: cce7f30efb3c46e8cede2dc15a66bca0b90294f0
Merged at: 2026-05-11T22:23:12Z
Cloudflare Workers build: Passed
Deployment: Approved and performed manually with Wrangler
Production version: 734f5282-affa-43b4-90ec-2f9d36a315c8
```

Website source:

```text
C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site
```

## Sources reviewed

- [[wiki/marketing/_marketing-quickref]]
- [[wiki/marketing/seo-strategy]]
- [[wiki/marketing/positioning]]
- [[wiki/marketing/copy-bank]]
- [[wiki/launch/website-deployment-plan]]
- [[2026-05-11-website-source-control-baseline]]
- Google Search Central SEO Starter Guide: `https://developers.google.com/search/docs/fundamentals/seo-starter-guide`
- Google Search Central developer SEO guide: `https://developers.google.com/search/docs/fundamentals/get-started-developers`
- Google Search Central technical SEO guide: `https://developers.google.com/search/docs/advanced/guidelines/get-started`
- Google Search Central robots meta tag docs: `https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag`

## Pages changed

- `game/index.html`
- `progress/index.html`
- `world-keys/index.html`
- `wiki/index.html`
- `press/index.html`
- `register/index.html`
- `robots.txt`
- `sitemap.xml`

## What changed

- Game page title/meta/structured-data language now leads with `Dungeon RPG`, `Creature Growth`, and `Shared World`.
- Progress page title/meta/structured data now reinforces roadmap intent around dungeon RPG gameplay, creature growth, inventory, and shared-world progress.
- World Keys page title/meta/structured data now clarifies that it is the account-linked browser-game hub for experiments, token rewards, and future side adventures.
- Wiki page now has canonical URL, Open Graph/Twitter metadata, and CollectionPage/Breadcrumb JSON-LD.
- Press page now has stronger shared-world RPG press-kit title, description, social metadata, and WebPage JSON-LD.
- Register page now has stronger conversion metadata and `noindex,follow`.
- `robots.txt` now blocks only `/admin/` and `/api/`, allowing public noindex pages to be crawled so search engines can see their noindex directives.
- `sitemap.xml` now uses the canonical homepage URL with trailing slash and updates lastmod values for the changed indexable pages.

## Checks run

- Extracted title, description, canonical, and robots metadata for core audited routes.
- Parsed all JSON-LD blocks across HTML files successfully.
- Parsed `sitemap.xml` as XML successfully.
- Ran local served preview at `http://127.0.0.1:8002/`.
- Browser checked these routes with zero warnings/errors:
  - `/`
  - `/game/`
  - `/progress/`
  - `/world-keys/`
  - `/wiki/`
  - `/blog/`
  - `/press/`
  - `/register/`
- Local route checks returned `200` for audited pages, `robots.txt`, and `sitemap.xml`.
- Ran `git diff --check`.
- Ran `npx wrangler deploy --dry-run`.
- Committed website changes locally as `1bb5dd8`.
- Pushed branch `codex/seo-site-growth-pass-20260511` to GitHub.
- Opened PR #2: `https://github.com/dodo-arcforge-interactive/the-world-beneath-site/pull/2`.
- Confirmed Cloudflare Workers build check passed.
- User approved proceeding after merge/deploy warning.
- Merged PR #2 into `main`.
- Fast-forwarded local `main` to merge commit `cce7f30efb3c46e8cede2dc15a66bca0b90294f0`.
- Confirmed Cloudflare did not auto-deploy after merge, then deployed manually with `npx wrangler deploy`.
- New production Worker version: `734f5282-affa-43b4-90ec-2f9d36a315c8`.
- Verified live metadata for `/game/`, `/progress/`, `/world-keys/`, `/wiki/`, `/press/`, and `/register/`.
- Verified live `robots.txt` and `sitemap.xml`.
- Browser-checked live edited routes with zero warnings/errors.

Wrangler dry-run result:

```text
Total Upload: 180.63 KiB / gzip: 34.23 KiB
```

## Risks

- Deployment is complete and live-verified.
- Wrangler uploaded 40 changed/new static assets because production was behind the merged source baseline, not only the eight SEO-edited files.
- Search result wording is not guaranteed; Google may rewrite titles or snippets.
- Register remains intentionally `noindex`; it is a conversion page, not an indexable SEO landing page.
- This pass did not perform new keyword-volume research or competitor validation.

## Memory-worthy notes

### Decision - 2026-05-11

The first page-by-page SEO pass should strengthen source metadata, structured data, crawl clarity, and conversion wording without changing the site's visual design or making new gameplay promises.

### Decision - 2026-05-11

The approved SEO/site growth pass was merged and deployed to production.

### Warning - 2026-05-11

Pages using `noindex` should not also be blocked in `robots.txt` if the goal is for search engines to see the noindex directive.

### Signal - 2026-05-11

Current source pages already had decent homepage, blog, community, and initiation SEO metadata. The weakest high-value gap was the public wiki page, which lacked canonical/social metadata and structured data.

## Do not promote to memory

- Do not treat this as proof of ranking improvement.
- Do not treat metadata edits as keyword validation.
- Do not deploy this branch until the user approves.

## Follow-up recommendations

1. Run a later dedicated keyword/competitor pass for search-volume validation.
2. Add a lightweight SEO validation script if this workflow repeats often.
3. Consider a second content-growth pass for blog internal links, press-kit completeness, and wiki entry landing pages.
