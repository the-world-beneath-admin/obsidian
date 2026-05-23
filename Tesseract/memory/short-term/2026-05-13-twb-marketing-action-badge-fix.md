# Task

Adjust TWB-Marketing tab badges so they indicate work needing attention, not total record counts.

# Result

Updated the Passwords tab badge to count incomplete account setups instead of total vault entries. Completing TWB Pinterest with username/email, password, login URL, and open URL now drops the Passwords badge from 7 to 6. When all accounts are ready, the Passwords badge disappears.

Archive no longer shows a tab badge because archived/responded posts are finished records, not work needing attention.

# Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\` rebuilt

# Checks run

- `npm run build` passed.
- `npm test -- --run` passed, 2 test files and 12 tests.
- `npm run package:win` passed.
- Packaged executable smoke test confirmed the Passwords badge starts at 7, completing TWB Pinterest drops it to 6, and Archive has no badge.
- Packaged executable smoke test confirmed completing all seeded accounts removes the Passwords badge.

# Cleanup performed

Temporary packaged-app smoke-test profiles under `%TEMP%\twb-marketing-needed-badge-smoke-*` and `%TEMP%\twb-marketing-badge-zero-smoke-*` were removed.

# Safety boundary confirmation

No social/platform APIs, account integrations, auto-posting, fixed-interval scanning, OpenAI API calls, or external notification integrations were added. This was a local UI semantics fix for the existing encrypted password vault.

# Risks

None known. Current “ready” rule requires username/email, saved password, login URL, open URL, and status **Saved**.

# Memory-worthy notes

TWB-Marketing tab badges should represent actionable outstanding work. Passwords badge means accounts still needing setup; Archive should not badge completed records.

# Do not promote to memory

Smoke-test temporary profile paths and test password values.

# Follow-up recommendations

If account setup grows more detailed, add a per-card checklist showing exactly which field is missing instead of a single **Needs setup** pill.
