# Task

Scope: shared TWB marketing operations tooling for The World Beneath and World Keys.

Remove Reddit from the Daily Queue, add personal-account daily queue items for LinkedIn, Facebook, and TikTok, then constrain personal-account content to TWB, World Keys, and AI-assisted development/workflow such as Obsidian/Codex integration.

# Result

Removed the Daily Queue Reddit item from seed/migration handling. This does not remove Reddit from Scout or Marketing scans.

Added personal-account Daily Queue items:

- Personal LinkedIn: first-person professional TWB or AI-dev post.
- Personal Facebook: first-person plain-language TWB or World Key post.
- Personal TikTok: first-person short video about TWB, World Keys, or AI-assisted development.

Updated personal queue prompts so copied prompts explicitly say personal-account posts may only cover The World Beneath, World Keys, or using AI/Obsidian/Codex to develop and organize the game. The prompt now blocks unrelated personal-brand, lifestyle, motivation, or filler social posts.

Added a Personal TikTok seed entry to the encrypted password/account vault.

Packaged latest build at:

```text
C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release-personal-queue\win-unpacked\TWB-Marketing.exe
```

# Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\data\dashboardSeed.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\main.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-marketing-personal-daily-queue.md`

# Checks run

- `npm run build` passed.
- `npm test -- --run` passed: 2 test files, 12 tests.
- `npx electron-builder --win --x64 --dir --config.directories.output=release-daily-queue` failed because that executable was open and locked.
- `npx electron-builder --win --x64 --dir --config.directories.output=release-personal-queue` passed.
- Packaged smoke test passed against `release-personal-queue\win-unpacked\TWB-Marketing.exe`: Daily Queue visible, Reddit daily item absent, LinkedIn/Facebook/TikTok personal items visible, and copied prompt includes the personal-account content boundary.

# Cleanup performed

Removed the temporary smoke-test Electron user-data folder after the test run.

Kept `release-personal-queue\win-unpacked\` because it contains the verified current executable.

# Safety boundary confirmation

No auto-posting, background scheduler, fixed-interval posting, platform API, account login automation, scraping, OpenAI API call, or notification integration was added.

All Daily Queue items remain manual: copy prompt, generate with Bob/Codex, open account URL, post manually, then mark posted.

# Risks

Multiple executable folders now exist because previously launched builds locked their output folders. The latest verified executable is under `release-personal-queue\win-unpacked`.

Existing local state will migrate when the updated executable runs, but any already-open older executable window will not show the newest queue changes.

# Memory-worthy notes

Decision: Reddit should not be a Daily Queue posting lane; it remains a Scout/Marketing discovery and review surface.

Decision: Personal-account content should only discuss TWB, World Keys, or AI-assisted development/workflow such as Obsidian/Codex integration.

Decision: Personal posts should use first-person developer/operator framing and should not become general lifestyle, personal-brand, motivation, or filler posts.

# Do not promote to memory

Do not promote transient packaging folder names or smoke-test implementation details.

# Follow-up recommendations

After confirming the newest window, close older TWB-Marketing windows and update the desktop shortcut to point at the latest verified executable or rebuild into the normal release folder once no executable is locked.
