# TWB-Marketing Executable Dashboard Milestone 1

## 1. Task

Build milestone 1 of the TWB-Marketing presence-agent app in `C:\Users\yrred\Desktop\Markeing\TWB-Marketing` as a local desktop operations dashboard for shared The World Beneath and World Key marketing work.

Requested follow-up changes during the task:

- Correct the original web-app direction into a desktop executable.
- Fix the blank packaged window.
- Separate the dashboard into tabs instead of one crowded view.
- Apply the requested minimalist dark UI with orange accent.
- Continue the remaining milestone 1 foundation until user help is needed.
- Record the user decision that this is a personal-use tool for this PC, with no installer needed for now.
- Replace the placeholder app icon with a TWB-symbol-derived grayscale/blue icon and a small `M` marketing badge.

Scope: shared marketing operations tooling for The World Beneath parent campaign and World Keys. This was not a game-dev task, not a World Key implementation task, and not a social automation task.

## 2. Result

Created and updated a local-first Electron + Vite + React + TypeScript dashboard packaged as a portable Windows executable:

```text
C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\TWB-Marketing-0.1.0-x64.exe
```

The user clarified this should remain a personal-use portable tool for this PC for now. No installer path is needed at this stage.

Current milestone state:

- Desktop executable launches and renders the dashboard.
- Data is separated into tabs: Overview, Reviews, Alerts, Readiness, Assets, and Archive.
- Visual design uses a minimalist dark UI with orange accent based on the provided readability sheet.
- Seed data, shared dashboard types, persistence helpers, and dashboard state helpers are split out of `src\App.tsx`.
- Review queue, draft queue, alert queue, readiness checklist, campaign lanes, forum tracker rows, asset/copy bank items, active tab, quiet-hours settings, alert mute, sleep throttle, digest settings, muted-until state, archived-record visibility, and last-export timestamp persist locally through Electron renderer localStorage.
- Local add/edit forms exist for campaign lanes, opportunities, drafts, alerts, readiness checklist items, forum tracker rows, and asset/copy bank items.
- Local archive/restore controls exist for all editable record groups.
- Archive actions set a local archived flag and show an undo affordance in the notice area.
- A global "Show archived" / "Hide archived" toggle exposes archived records inline.
- A dedicated Archive tab groups archived records by record type and provides restore controls.
- JSON export and import controls exist for local dashboard state.
- JSON import now uses a testable validation helper with field and enum checks before replacing local state.
- Invalid JSON imports preserve existing local state and fail visibly.
- A local backup reminder/status strip now appears on Overview, with a "Backup due" header pill until a local JSON export has been prepared.
- Exporting records `lastExportAt` locally and changes the backup state to current.
- A reset control restores the seeded local milestone state.
- The packaged app now uses a grayscale/blue TWB-symbol-derived icon with a small `M` badge to identify it as the marketing dashboard.
- The renderer favicon now uses `public\favicon.png`; the packaged executable icon uses `public\icon.ico`.
- Vitest coverage was added for archive helpers, ID allocation, JSON import validation, enum rejection, and same-session backup date math.

The dashboard still uses local/mock data only and visibly models campaign overview, opportunity/rule-risk review, draft approval, alert center, quiet-hours controls, snooze/mute, platform readiness, forum outreach placeholder, asset/copy bank preview, and safety indicators.

## 3. Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\package.json`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\package-lock.json`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\index.html`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\vite.config.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\public\favicon.png`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\public\icon.ico`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\public\twb-marketing-icon.png`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.css`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\index.css`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\types.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\data\dashboardSeed.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\hooks\usePersistentState.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\dashboardState.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\dashboardState.test.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\main.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\dev.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\preload.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\TWB-Marketing-0.1.0-x64.exe`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-app-dev-dashboard-milestone-1.md`

## 4. Checks run

- `npm install --save-dev vitest` completed.
- `npm run lint` passed.
- `npm run test` passed with 1 test file and 6 tests.
- `node --check electron\main.cjs` passed.
- `node --check electron\dev.cjs` passed.
- `node --check electron\preload.cjs` passed.
- `npm run build` passed.
- `npm run package:win` passed and rebuilt the portable executable.
- Latest packaged executable smoke check with a temporary user-data directory confirmed:
  - dashboard title rendered as `TWB-Marketing Dashboard`,
  - tabs rendered as Overview, Reviews, Alerts, Readiness, Assets, and Archive,
  - renderer favicon resolved to `./favicon.png`,
  - backup due state rendered on a fresh temporary profile.
- Packaged executable smoke check with a temporary user-data directory confirmed:
  - dashboard rendered,
  - tabs rendered as Overview, Reviews, Alerts, Readiness, Assets, and Archive,
  - backup strip initially showed backup recommended,
  - export action recorded `lastExportAt` in localStorage,
  - backup strip changed to "Backup current" / "Last local JSON export was today.",
  - "Backup due" header pill disappeared after export,
  - export notice appeared as "Local dashboard JSON export prepared."
- Previous packaged executable Archive-tab smoke check confirmed:
  - archiving a campaign persisted the archived flag,
  - Archive tab count updated,
  - Archive Review panel rendered,
  - archived campaign appeared under the Campaign lanes group,
  - grouped restore cleared the archived flag,
  - empty state appeared after restore,
  - reset returned active tab to Overview and restored seeded campaign lanes.
- Previous packaged executable invalid-import smoke check confirmed:
  - malformed dashboard JSON shows `Import failed. Use a JSON export from this dashboard.`,
  - existing local campaign data remains intact after failed import.
- Safety scan over `src`, `electron`, and `package.json` found no app fetch calls, OpenAI calls, platform API integrations, notification APIs, fixed runtime intervals, credential handling, cookie handling, scraping paths, social SDKs, or shell external-opening paths. Remaining matches were localStorage, browser FileReader/Blob export helpers, mock seed labels, and dev helper process code for launching Vite during development.

Historical milestone checks:

- Initial package attempt failed because Electron Builder tried to extract `winCodeSign` symlinks without Windows symlink privileges.
- Packaging passed after disabling code-signing discovery and signing/editing for the unsigned local portable build.
- Initial packaged executable launched blank because Vite emitted absolute `/assets/...` paths.
- Blank packaged window was fixed by setting Vite `base: './'`.

## 5. Cleanup performed

- Stopped temporary Electron smoke-test processes created by this task.
- Used temporary smoke-test user-data directories and removed them after verification.
- Removed generated `dist\` build output after packaging and verification.
- Removed Electron Builder intermediate output:
  - `release\win-unpacked\`
  - `release\builder-debug.yml`
- Removed stale generated `public\favicon.svg` after switching the renderer to the TWB-derived PNG favicon.
- Confirmed no `TWBMarketingSmoke-*` temp folders remained.
- No generated screenshot files were created on disk.
- Kept `release\TWB-Marketing-0.1.0-x64.exe` because it is the requested executable deliverable.
- Kept `node_modules\` because it is the installed dependency tree needed for local development/builds after `npm install`.
- Kept the earlier `memory\reports\app-dev\2026-05-12-dashboard-milestone-1.md` because it was written before the short-term guidance update and reports should not be deleted.

## 6. Safety boundary confirmation

- No auto-posting was built.
- No fixed-interval posting was built.
- No social, forum, store, notification, or OpenAI API integration was added.
- No social account login, credentials, tokens, cookies, or private account data were added.
- No scraping libraries or automation libraries were added.
- Electron preload exposes no desktop bridge/API.
- Electron renderer has Node integration disabled, context isolation enabled, sandbox enabled, menu hidden, and window-open requests denied.
- Alerting is local UI/state only.
- Persistence is local renderer localStorage only.
- JSON import/export is local user file handling only.
- Archive/restore is local record visibility only; it does not delete files or external data.
- Drafts remain manual approval items only.
- Blocked or no-advertising communities are represented as blocked/review-only, not as evasion targets.

## 7. Risks

- The executable is a portable unsigned local build for personal use on this PC. Windows may warn when opening it, but no installer is currently desired.
- The app icon is derived from `twb-symbol-transparent.png` from the TWB website assets, recolored locally into grayscale/blue with an `M` badge. It is fit for this personal tool but can still be replaced if a stricter final brand asset is chosen later.
- Local persistence uses versioned localStorage keys with no multi-version migration layer yet.
- JSON import validation is stricter than before but still does not cover future schema migrations.
- Archive is reversible and safer than delete, but there is no permanent deletion path by design.
- Quiet-hours behavior is visible and locally stateful but not connected to real time, background gathering, or external notifications.
- Backup reminder is local UI state only; it does not automatically create backups.
- Forum outreach tracker uses manual rule states; no approved public-source intake workflow exists yet.

## 8. Memory-worthy notes

- Milestone 1 is implemented as a local executable dashboard foundation at `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\TWB-Marketing-0.1.0-x64.exe`.
- User decision: keep TWB-Marketing as a personal-use portable desktop tool on this PC for now; no installer is needed.
- The app uses Electron around the Vite/React renderer and is packaged as a portable Windows executable.
- The UI separates data into six tabs: Overview, Reviews, Alerts, Readiness, Assets, and Archive.
- The visual scheme follows the orange accent dark UI direction from the provided readability sheet.
- The app has split seed data/types, a reusable local persistence hook, and a reusable dashboard state helper module.
- Dashboard queue/status controls, campaign lanes, readiness checks, forum tracker rows, asset/copy bank items, selected tab, archived visibility, quiet-hours controls, and last export timestamp persist locally in Electron localStorage.
- The app supports local add/edit forms, reversible archive/restore, grouped archive review, local JSON export/import, stricter import validation, local backup status, and reset to seeded milestone state.
- The app icon now uses a TWB-symbol-derived grayscale/blue variant with a small `M` badge for marketing identification.
- Automated Vitest coverage now exists for core local state helpers and backup date math.
- The app currently has no backend, auth, database, platform API, social SDK, OpenAI SDK, notification integration, fixed posting schedule, scraping path, desktop bridge, or auto-posting path.

## 9. Do not promote to memory

- Do not treat the seeded mock opportunities, alert titles, forum rows, or draft copy as real campaign evidence.
- Do not treat the current dashboard layout as final product design beyond milestone 1.
- Do not promote generated Vite scaffold details, build asset hashes, local smoke-test ports, Electron Builder cache paths, or temporary user-data folder names.
- Do not promote the pre-guidance report destination as the ongoing process.
- Do not promote the current app icon as the whole-project brand identity; it is the personal-use marketing-dashboard icon variant.

## 10. Follow-up recommendations

- Keep the current portable-only workflow unless the user later decides to distribute the tool beyond this PC.
- Replace or refine the app icon only if a stricter final TWB marketing-dashboard icon asset is chosen later.
- Add deeper schema migration support before the JSON export format becomes important.
- Define the approved public-source intake model before adding any opportunity-gathering features.
- Add more UI-level regression tests if dashboard workflows continue to grow.
- Keep integrations blocked until a named platform workflow, official rules review, permission model, and explicit user approval exist.
