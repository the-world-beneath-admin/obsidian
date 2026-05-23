# Task

Scope: shared TWB marketing operations tooling for The World Beneath and World Keys.

Plan and add daily posts for The World Beneath website forum under an administrative account. The forum posts should mirror and consolidate the useful information from the other daily publishing lanes.

# Result

Updated the Daily Queue seed so the website forum lane is now an official administrative roundup lane:

- Platform: Website Forum
- Account label: TWB Forum Admin
- Title: Daily TWB forum admin roundup
- Purpose: consolidate daily YouTube, Pinterest, Discord, X, itch.io, Reddit, main-game, and World Key updates into one official home-base forum post.

Added a TWB Forum Admin seed entry to the encrypted password/account vault so the queue can open the correct account/profile URL once configured.

Added a small migration for existing local Daily Queue state so the older generic "Daily website forum update" item upgrades to the forum-admin roundup instead of requiring a full dashboard reset.

Opened the newly packaged executable for the user after confirming the screenshot was from the older running executable.

# Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\data\dashboardSeed.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\main.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-marketing-forum-admin-daily-queue.md`

# Checks run

- `npm run build` passed.
- `npm test -- --run` passed: 2 test files, 12 tests.
- `npx electron-builder --win --x64 --dir --config.directories.output=release-daily-queue` passed.
- Packaged Electron smoke test passed against `release-daily-queue\win-unpacked\TWB-Marketing.exe`: Daily Queue tab visible and TWB Forum Admin roundup visible.

# Cleanup performed

Removed the temporary smoke-test Electron user-data folder after the test run.

Kept `release-daily-queue\win-unpacked\` because it contains the verified updated executable.

# Safety boundary confirmation

No auto-posting, background scheduler, fixed-interval posting, social API, account login automation, scraping, OpenAI API call, or notification integration was added.

The forum-admin lane is still manual: copy prompt, generate content in Bob/Codex, open account URL, post manually, then mark posted.

# Risks

The normal old executable window may still be open from `release\win-unpacked`, and that copy does not show the Daily Queue tab. The updated copy is under `release-daily-queue\win-unpacked`.

The actual website forum admin URL may need to be refined once the exact forum/admin path is confirmed.

# Memory-worthy notes

Decision: The World Beneath website forum should be the official daily recap/home-base lane.

Decision: Forum posts should consolidate and mirror useful information from the other daily lanes instead of creating separate noisy content.

Decision: The forum lane should run under a TWB administrative account, represented in the local password/account vault as `TWB Forum Admin`.

# Do not promote to memory

Do not promote transient packaging paths or smoke-test implementation details.

# Follow-up recommendations

After confirming the updated window, close the old executable and replace/update the desktop shortcut if it still points at `release\win-unpacked`.

Confirm the exact website forum/admin posting URL and update the TWB Forum Admin vault entry/profile URL if needed.
