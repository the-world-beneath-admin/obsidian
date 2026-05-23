# 2026-05-13 TWB-Marketing Scout Simplification

## 1. Task

Simplify TWB-Marketing around the actual desired workflow: Scout-driven opportunity discovery and response tracking.

Scope: shared marketing/account operations for The World Beneath and World Keys.

## 2. Result

The visible app workflow is now:

- Overview
- Scout
- Archive

Removed from the visible navigation:

- Reviews
- Alerts
- Readiness
- Assets

Overview was simplified to Scout-focused status only. The top status/control strip was hidden because it was no longer useful for the simplified workflow.

Scout now has a **Responded** button on opportunity cards and in the draft review window. Pressing it opens a confirmation dialog; only after confirming **Yes, I responded** does the post move out of Scout and into Archive.

Archive now shows posts marked **Responded**, not general old dashboard records.

## 3. Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.css`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\types.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\lib\dashboardState.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\README.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\TWB-Marketing-0.1.0-x64.exe`

## 4. Checks run

- `npm run lint` passed.
- `npm run test` passed: 2 test files, 11 tests.
- `npm run build` passed.
- `npm run package:win` passed.
- Packaged Electron smoke test passed:
  - visible tabs are Overview, Scout, Archive,
  - removed tabs are not visible,
  - top status/key strip is not visible,
  - Responded confirmation opens,
  - confirmed responded post appears in Archive.
- Safety scan found no OpenAI API calls, OAuth wiring, cookies, passwords, fixed intervals, or posting API paths.

## 5. Cleanup performed

Removed generated package/build clutter after rebuilding:

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\dist`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\builder-debug.yml`
- temporary `TWBMarketingSmoke-*` runtime profiles under `%TEMP%`

Kept the portable executable and source files.

## 6. Safety boundary confirmation

- No auto-posting was added.
- No social account connection or login was added.
- No OpenAI API or Codex OAuth integration was added.
- No fixed-interval or background scouting was added.
- Scout remains user-triggered.
- Posting remains manual; Responded is only a local tracking state.

## 7. Risks

- Legacy local storage may still contain older Reviews/Alerts/Readiness/Assets data, but those surfaces are no longer visible in the simplified app.
- The source code still contains some legacy editor sections behind non-visible tabs; this is low user risk but should be cleaned in a later source-pruning pass if the simplified direction remains stable.
- Responded relies on user honesty/accuracy; the confirmation dialog reduces accidental marking but cannot prove a post was actually made.

## 8. Memory-worthy notes

- Decision: TWB-Marketing should center on manual on-demand scouting, local Gemma drafting, manual posting, and Responded archive tracking.
- Decision: Reviews, Alerts, Readiness, and Assets are not useful for the user's current mental model and should stay out of the visible workflow unless a concrete need returns.
- Decision: Archive means posts the user marked as Responded.

## 9. Do not promote to memory

- Temporary smoke-test opportunity title and fixture data.
- Old dashboard implementation details unless needed for a cleanup task.

## 10. Follow-up recommendations

- Next app step should be source-pruning: remove the hidden legacy Reviews/Alerts/Readiness/Assets code paths once the user confirms this simplified workflow feels right.
- Add optional response notes later, such as "what I posted" or "outcome," only if the user actually wants tracking beyond Responded.
- Consider adding filters for New/Drafted/Responded once the queue grows.
