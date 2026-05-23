# TWB Marketing Daily Queue Repackage - 2026-05-13

## Task

Investigate why the TWB-Marketing desktop app did not show the Daily Queue tab after daily post work had been added.

## Result

The Daily Queue code and seed data were still present in source. The visible app was running an older packaged executable that did not include the current built `dist`.

Rebuilt the Windows portable desktop app:

`C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\TWB-Marketing.exe`

Created a desktop shortcut:

`C:\Users\yrred\Desktop\TWB-Marketing Dashboard.lnk`

The Daily Queue tab should appear between Marketing and Passwords after the app is closed and relaunched from that shortcut or rebuilt executable.

## Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\dist\`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\`
- `C:\Users\yrred\Desktop\TWB-Marketing Dashboard.lnk`

## Checks run

- Searched source for Daily Queue and daily post seed data.
- Ran `npm run package:win`.
- Confirmed rebuilt executable timestamp updated to 2026-05-13 1:44 PM.
- Confirmed built `dist` contains Daily Queue content.
- Checked desktop shortcut targets and created a correct app shortcut.

## Cleanup performed

No temporary files were created.

## Safety boundary confirmation

No platform APIs, account integrations, auto-posting, or social automation were added. This was a local rebuild/shortcut correction only.

## Risks

If an older app window remains open, it will continue showing the old tab set until closed and relaunched.

## Memory-worthy notes

The Daily Queue feature exists in source and current `dist`, but users may see missing tabs if launching an older packaged executable or stale shortcut.

## Do not promote to memory

Do not promote this as a product decision; it is a packaging/shortcut correction.

## Follow-up recommendations

Use a single stable desktop shortcut for TWB-Marketing to avoid launching side-build folders.
