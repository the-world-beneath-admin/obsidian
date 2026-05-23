# Task

Add a password manager tab to the TWB-Marketing personal desktop app for TWB and Personal social/account lanes.

# Result

Implemented a new **Passwords** tab in `C:\Users\yrred\Desktop\Markeing\TWB-Marketing` with seeded entries for TWB Pinterest, Gmail, Reddit, YouTube, itch.io, plus Personal LinkedIn and Facebook.

Passwords are stored through Electron `safeStorage` in an encrypted per-user desktop vault file, not in React local storage and not in dashboard JSON exports. The UI supports adding/editing account entries, saving/updating passwords, copying a saved password on demand, deleting entries, and opening configured social/login URLs. The app still does not log in, sync, post, or connect platform APIs.

# Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\main.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\preload.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.css`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\types.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\electron-api.d.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\dashboardState.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\` rebuilt

# Checks run

- `npm run build` passed.
- `npm test -- --run` passed, 2 test files and 12 tests.
- `npm run package:win` passed and rebuilt `release\win-unpacked\TWB-Marketing.exe`.
- Packaged executable smoke test confirmed the **Passwords** tab and 7 seeded vault entries.
- Packaged executable vault smoke test saved, listed, revealed, and deleted a temporary encrypted test entry in a temporary app profile.

# Cleanup performed

Temporary smoke-test app profiles under `%TEMP%\twb-marketing-vault-*` were removed. No real account passwords were used or stored during verification.

# Safety boundary confirmation

No auto-posting, fixed-interval posting, platform API connections, social logins, scraping of private/gated data, OpenAI API calls, external notification integrations, rule evasion, fake engagement, or spam features were added.

The credential feature is local-only and encrypted with the current Windows user context through Electron safe storage. Passwords are copied only after explicit button click and are excluded from the dashboard JSON export/import path.

# Risks

- The vault is tied to the local Windows user profile. Moving the encrypted vault file to another PC or Windows account may make saved passwords unreadable.
- Clipboard copy necessarily places the selected password on the system clipboard until overwritten.
- This is a personal local vault, not a cross-device password manager with sync, breach monitoring, or browser autofill.

# Memory-worthy notes

- TWB-Marketing now has a Passwords tab for account launcher and encrypted credential storage.
- Initial account inventory: TWB Pinterest, Gmail, Reddit, YouTube, itch.io; Personal LinkedIn and Facebook.
- Password storage decision: use local Electron/Windows safe storage, exclude secrets from dashboard JSON exports, and avoid social/platform login integrations.

# Do not promote to memory

- Temporary smoke-test password value and test profile paths.
- Build artifact timestamps.

# Follow-up recommendations

- Add TWB Discord and website/forum account entries next if the user wants them in the vault.
- Consider adding an optional clipboard-clear timer only if the user wants that behavior, since it can overwrite something they copied afterward.
