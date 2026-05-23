# Task

Fix TWB-Marketing Passwords tab behavior where **Edit** appeared to stop working after several account entries were completed.

# Result

Updated the Passwords tab edit flow so clicking **Edit** opens the editor, scrolls the editor into view, focuses the first editable field, and shows a notice naming the account being edited. This prevents lower-list edits from silently populating the form above the current scroll position.

# Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\` rebuilt

# Checks run

- `npm run build` passed.
- `npm test -- --run` passed, 2 test files and 12 tests.
- `npm run package:win` passed.
- Packaged executable smoke test completed the first three account entries, clicked **Edit** on a lower account, and confirmed the editor opened, populated, scrolled into view, and focused the form.

# Cleanup performed

Temporary packaged-app smoke-test profile under `%TEMP%\twb-marketing-edit-scroll-smoke-*` was removed.

# Safety boundary confirmation

No social/platform APIs, account integrations, auto-posting, fixed-interval scanning, OpenAI API calls, or external notification integrations were added. This was a local UI behavior fix only.

# Risks

None known.

# Memory-worthy notes

Password tab edit actions should always make the editor visible and focused, especially after the user has scrolled down the account list.

# Do not promote to memory

Smoke-test temporary profile paths and test password values.

# Follow-up recommendations

If account list grows longer, consider moving the edit form into a modal or side panel so edits are always visually anchored to the clicked row.
