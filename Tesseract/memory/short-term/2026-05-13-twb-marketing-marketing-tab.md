# 2026-05-13 TWB-Marketing Marketing Tab

## 1. Task

Separate explicit marketing-post opportunities from the helpful-reply Scout queue.

Scope: shared marketing/account operations for The World Beneath and World Keys.

## 2. Result

Added a visible **Marketing** tab between Scout and Archive.

- Scout now shows helpful reply opportunities only.
- Marketing shows direct-promotion lanes only.
- Existing/scanned items from marketing-safe sources, including `r/indiegames`, are classified into Marketing instead of Scout.
- Added marketing-safe sources:
  - `r/indiegames marketing posts`
  - `r/playmygame post lane`
  - `itch.io Release Announcements`
  - `itch.io Games board`
  - `itch.io Get Feedback`
- The app reconciles saved source settings with the default registry so new sources appear even if old local source state exists.
- Local Gemma prompt logic now distinguishes helpful replies from direct marketing posts.
- Packaging command now builds the unpacked desktop executable folder instead of the single-file portable target, because the portable NSIS stage hung.

## 3. Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\package.json`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\main.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\data\sourceRegistry.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\dashboardState.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\opportunityScout.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\opportunityScout.test.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\types.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\TWB-Marketing.exe`

## 4. Checks run

- Verified marketing source URLs returned `200`:
  - `https://itch.io/board/10022/release-announcements`
  - `https://itch.io/board/10024/games`
  - `https://itch.io/board/10021/get-feedback`
  - `https://www.reddit.com/r/playmygame/new.json?limit=1`
  - `https://www.reddit.com/r/indiegames/new.json?limit=1`
- `npm run lint` passed.
- `npm run test` passed: 2 test files, 12 tests.
- `npm run build` passed.
- `npm run package:win` passed after switching to unpacked directory packaging.
- Packaged Electron smoke test passed:
  - Overview, Scout, Marketing, Archive tabs visible.
  - Reviews, Alerts, Readiness, Assets not visible.
  - Helpful fixture appeared in Scout only.
  - Marketing fixture appeared in Marketing only.
- Safety scan found no OpenAI API calls, OAuth wiring, cookies, passwords, posting API paths, or fixed intervals. Matches for fake engagement/upvote were inside prohibition prompts/checks only.

## 5. Cleanup performed

Removed generated build leftovers:

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\dist`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\builder-debug.yml`
- temporary `TWBMarketingSmoke-*` runtime profiles under `%TEMP%`

Kept `release\win-unpacked\` because it is now the current executable build. The older single-file `release\TWB-Marketing-0.1.0-x64.exe` could not be removed because Windows reported it was in use; treat it as stale and prefer `release\win-unpacked\TWB-Marketing.exe`.

## 6. Safety boundary confirmation

- No auto-posting was added.
- No account login or social API connection was added.
- No OpenAI API or Codex OAuth integration was added.
- Marketing tab only drafts manual posts for sources where direct promotion appears allowed.
- Posting remains manual through Open Social and Copy response.
- The app still uses user-triggered scanning only.

## 7. Risks

- Community rules can change; source guardrails should be reviewed periodically.
- Marketing tab has source-level opportunities rather than proof that a specific post should be made today.
- The old single-file executable is stale if still present; use `release\win-unpacked\TWB-Marketing.exe`.
- Some legacy hidden code remains from old tabs and can be pruned later.

## 8. Memory-worthy notes

- Decision: TWB-Marketing now separates helpful-reply scouting from explicit marketing-post opportunities.
- Decision: `r/indiegames` belongs in the Marketing lane, not the helpful Scout lane.
- Decision: Packaging should use unpacked desktop executable output for now because it is personal-use and avoids NSIS portable hangs.

## 9. Do not promote to memory

- Smoke-test fixture names.
- Temporary packaging failure details beyond the durable note that unpacked packaging is now preferred.

## 10. Follow-up recommendations

- Add user-editable source rules before expanding beyond Reddit and itch.io.
- Add a "draft title" field for Marketing posts, since Reddit/itch marketing posts need titles as well as bodies.
- Add a review date to each marketing source so stale rule assumptions are easy to spot.
