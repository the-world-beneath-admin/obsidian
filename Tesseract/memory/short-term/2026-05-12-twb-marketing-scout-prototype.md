# TWB-Marketing Reddit/itch.io Scout Prototype

## Task

Build the first working forum-skimming prototype for TWB-Marketing: scan Reddit and itch.io public/community surfaces, queue possible helpful reply opportunities for user review, and provide a rules-aware draft response workflow with copy/open actions.

Scope: shared marketing/account operations for The World Beneath and World Keys. This is not game development, not auto-posting, and not a social account connection task.

## Result

Implemented a new `Scout` tab in the TWB-Marketing desktop app.

Current prototype behavior:

- Scans configured public Reddit and itch.io sources through a narrow Electron main-process bridge.
- Default sources:
  - `r/gamedev`
  - `r/indiegames`
  - `r/rpg_gamers`
  - itch.io community front page
  - itch.io Questions & Support
  - itch.io Help Wanted or Offered
- Shows source cards with enabled toggles, rules summaries, access method, no-signature/no-default-link flags, and open-source buttons.
- Queues scanned opportunity candidates with:
  - source/platform,
  - title,
  - author/source label,
  - excerpt,
  - matched signals,
  - helpful angle,
  - rule risk,
  - link/signature policy,
  - status.
- Provides per-opportunity actions:
  - Review,
  - Draft response,
  - Open Social,
  - Dismiss.
- Draft response opens a modal/subwindow-style review surface with:
  - readable draft text,
  - format note,
  - safety note,
  - Copy response,
  - Open Social.
- Drafting is currently a local rules-aware prototype helper, not an external LLM call. The UI/flow is ready for a later API-backed LLM provider once the user chooses the key/provider and secret-handling plan.
- Drafts are also copied into the existing local Draft Response Queue with `Needs review` status.
- Export/import now includes scanned opportunities when present.
- Packaged executable was rebuilt:
  - `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\TWB-Marketing-0.1.0-x64.exe`

## Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.css`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\types.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\data\sourceRegistry.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\electron-api.d.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\dashboardState.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\opportunityScout.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\opportunityScout.test.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\main.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\preload.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\TWB-Marketing-0.1.0-x64.exe`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-marketing-scout-prototype.md`

## Checks run

- Probed public source availability with Node `fetch`:
  - Reddit public JSON endpoint returned data.
  - itch.io community/board pages returned public HTML.
  - itch.io RSS/game feeds were available but not used for forum-skimming.
- `npm run lint` passed.
- `npm run test` passed with 2 test files and 8 tests.
- `node --check electron\main.cjs` passed.
- `node --check electron\dev.cjs` passed.
- `node --check electron\preload.cjs` passed.
- `npm run build` passed.
- `npm run package:win` passed and rebuilt the portable executable.
- Packaged executable smoke test with temporary user-data directory confirmed:
  - app rendered with tabs: Overview, Scout, Reviews, Alerts, Readiness, Assets, Archive,
  - Scout tab rendered,
  - 6 source cards rendered,
  - live scan completed,
  - 48 public opportunity candidates appeared during the test run,
  - Draft response opened the draft review modal,
  - draft included useful-first/no-default-link guardrails.
- Safety scan over `src`, `electron`, and `package.json` found expected public fetch/open-link bridge code only. No OpenAI calls, credentials, cookies, private account access, auto-posting, fixed intervals, notification APIs, or social login paths were added.

## Cleanup performed

- Removed generated `dist\` after packaging and verification.
- Removed Electron Builder intermediate output:
  - `release\win-unpacked\`
  - `release\builder-debug.yml`
- Removed temporary `TWBMarketingSmoke-*` smoke-test profiles.
- Kept `release\TWB-Marketing-0.1.0-x64.exe` as the requested personal-use executable.

## Safety boundary confirmation

- No auto-posting was built.
- No fixed-interval scan/post loop was built.
- No social account login or account connection was added.
- No credentials, tokens, cookies, or private account data were requested or stored.
- The scanner uses configured public Reddit JSON and public itch.io HTML pages only.
- The Electron scan bridge allowlists scan hosts to Reddit and itch.io.
- The Open Social bridge allowlists Reddit and itch.io URLs only.
- Drafts remain manual copy/paste aids.
- The draft helper avoids default project links/signatures and labels rule risk.
- No OpenAI API or other LLM API call was added in this pass.

## Risks

- Reddit and itch.io public page structures/rate limits may change; source scanners should fail visibly and stay user-triggered.
- itch.io forum parsing is a limited public-HTML parser; it does not read full thread bodies yet.
- Reddit scanning currently uses public subreddit `new.json` endpoints without OAuth, which may be rate-limited or blocked by Reddit policy changes.
- Drafting is local/template-based for now, not actual LLM-backed drafting.
- The opportunity signal scoring is deliberately simple and will need tuning to reduce noise.
- Community rules are represented as source-level guardrails, not per-thread moderator verification.

## Memory-worthy notes

- TWB-Marketing now has a working Scout prototype for Reddit + itch.io opportunity discovery.
- First live discovery lane is Reddit and itch.io only.
- The intended response style is help-first, no default forum signature, no default project link, and no direct game advertising.
- Draft review flow now supports Copy response and Open Social while preserving manual posting.
- Future LLM drafting needs an explicit API/key/secret-handling decision before implementation.

## Do not promote to memory

- Do not promote the 48 scan-result count as a durable metric; it was a one-time smoke-test result.
- Do not treat any scanned live post as endorsed campaign evidence.
- Do not treat source-level rule summaries as a substitute for reviewing individual community rules.
- Do not promote the local template draft helper as the final LLM implementation.

## Follow-up recommendations

- Add a real LLM provider integration only after choosing API provider, key storage, and privacy boundaries.
- Add per-source query tuning and per-thread rule notes.
- Add a "blocked because self-promo" rule result state for sources/threads that forbid even soft mentions.
- Add saved source presets for specific approved subreddits and itch.io boards.
- Consider scanning full itch.io thread pages only if public HTML parsing remains acceptable and rate-limited/user-triggered.
