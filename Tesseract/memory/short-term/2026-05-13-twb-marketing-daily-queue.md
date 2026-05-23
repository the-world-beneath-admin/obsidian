# Task

Scope: shared TWB marketing operations tooling for The World Beneath and World Keys.

Add a daily publishing queue to the TWB-Marketing desktop app so Bob/Codex can be prompted to create daily social/video update packages from the correct Obsidian lanes.

# Result

Added a new Daily Queue tab to the desktop dashboard.

The queue starts with local/manual items for TWB YouTube, Pinterest, Discord, website forum, X, itch.io, and Reddit. Each item tracks platform, account/open URL, scope, content type, cadence, slot, objective, Obsidian source/template references, notes, status, and last posted timestamp.

Each queue item has actions to copy a Bob/Codex prompt, open the configured account URL, mark draft ready, mark manually posted, edit, and archive/restore. The copied prompt asks Bob to read the listed Obsidian lanes and create a platform-ready package while preserving TWB/World Key boundaries and manual posting rules.

Packaged build was created at:

```text
C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release-daily-queue\win-unpacked\TWB-Marketing.exe
```

The normal `release\win-unpacked` output could not be overwritten because the old app executable was still running.

# Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\types.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\data\dashboardSeed.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\dashboardState.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.css`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-13-twb-marketing-daily-queue.md`

# Checks run

- `npm run build` passed.
- `npm test -- --run` passed: 2 test files, 12 tests.
- `npm run package:win` built the app but failed during packaging because `release\win-unpacked\d3dcompiler_47.dll` was locked by the running old executable.
- `npx electron-builder --win --x64 --dir --config.directories.output=release-daily-queue` passed.
- Packaged Electron smoke test passed against `release-daily-queue\win-unpacked\TWB-Marketing.exe`: Daily Queue tab visible, seeded items visible, and Posted action updated queue state.
- Safety grep found no new OpenAI/social API/scheduler/auto-posting code paths; matches were boundary text and local Daily Queue functions.

# Cleanup performed

Removed the temporary smoke-test Electron user-data folder after the test run.

Kept `release-daily-queue\win-unpacked\` because it contains the verified updated executable. No screenshots, throwaway logs, or scratch files were intentionally left behind.

# Safety boundary confirmation

No auto-posting was added.

No fixed-interval posting or background scheduler was added.

No social platform APIs, account connections, scraping libraries, OpenAI API calls, or external notification integrations were added.

The Daily Queue is local/manual state only. It creates prompts for Bob/Codex, opens configured URLs, and lets the user mark posted after manual publication.

# Risks

The user has existing local dashboard state. The new Daily Queue key seeds automatically when the updated app launches, but the currently running old executable will not show the new tab until replaced or a newer build is opened.

The normal executable folder was not overwritten because the old app was open. The updated build is in `release-daily-queue\win-unpacked\`.

Dedicated YouTube/Pinterest/video template files were not found by filename in the vault search. The queue points at existing approved marketing/copy/trailer/source-lane notes and leaves template reference fields editable.

# Memory-worthy notes

Decision: Daily Queue should remain a manual content command center, not an automated posting scheduler.

Decision: Daily content prompts should read Obsidian lane/source notes first and produce platform-ready packages for manual posting.

Initial queue lanes: YouTube video, Pinterest pin, Discord announcement, website forum update, X short post, itch.io devlog/update, and Reddit safety review.

Warning: Reddit should not be treated as a forced daily posting lane. The seeded Reddit item is a rule-safe review/check item and may recommend skipping.

# Do not promote to memory

Do not promote build paths or transient smoke-test implementation details.

Do not promote the failed `release\win-unpacked` overwrite as a product issue; it was caused by the old executable still running.

# Follow-up recommendations

Close the currently running old TWB-Marketing app, then rebuild/copy the verified Daily Queue build into the normal `release\win-unpacked` location if the desktop shortcut should keep pointing there.

Create or consolidate explicit platform templates for YouTube, Pinterest, Discord announcements, website forum updates, X posts, and itch.io devlogs if the existing pre-made templates are stored under unexpected names.

Consider adding a "reset today's posted marks" control later if multiple posts per day become common.
