# TWB Marketing Daily Prompt Audit - 2026-05-13

## Task

Audit Daily Queue prompts after the YouTube package produced an internal/template-style asset instead of a postable video, and fix the Pinterest prompt copy failure.

Scope: Shared TWB-Marketing desktop app / daily content queue.

## Result

Updated the Daily Queue prompt builder so platform prompts now require postable deliverables, not just planning packages.

YouTube video prompts now require:

- Actual rendered MP4 when HyperFrames is available.
- Audience-facing visible text only.
- Internal grounding notes separated from public assets.
- Existing local audio search under `C:\Users\yrred\Desktop\Audio Tracks\archive` and `C:\Users\yrred\Desktop\Unity\TWB_Phase1_IdlePrototype\Music`.
- A trimmed/faded/normalized with-audio MP4 when a suitable track exists.
- Music-generation prompts and an explicit blocker note if audio cannot be added.

Pinterest/image prompts now require an actual postable image asset when tooling is available, rather than stopping at an image brief.

TikTok/short-video prompts now prefer an actual vertical render with sound when tooling is available.

Clipboard copying now uses an Electron IPC clipboard bridge in the desktop app, with browser clipboard and textarea fallback for dev mode. This should fix Daily Queue prompt copying, including the Pinterest prompt.

Rebuilt the Windows desktop app at:

`C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\TWB-Marketing.exe`

## Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\main.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\electron\preload.cjs`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\electron-api.d.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\App.tsx`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\src\data\dashboardSeed.ts`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\dist\`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\release\win-unpacked\`

## Checks run

- `npm run build`
- `npm test`
- `npm run package:win`
- Verified rebuilt executable timestamp.
- Verified desktop shortcut still targets the rebuilt executable.
- Verified built `dist` contains the new postable-asset prompt language and clipboard bridge references.

## Cleanup performed

No temporary artifacts were created.

## Safety boundary confirmation

No auto-posting, platform API posting, social account integration, scraping, fake engagement, or rule evasion was added.

The app still produces/copies prompts and opens platform links manually; posting remains manual.

## Risks

If the old desktop app window remains open, it will keep running old code until closed and relaunched.

Prompt generation is stricter, but actual image/video creation still depends on the tools available in the receiving Codex session.

## Memory-worthy notes

Daily Queue prompts should distinguish internal source grounding from public/postable assets.

Video daily posts should explicitly request actual rendered MP4 files and sound/music handling, not only scripts or storyboards.

Electron desktop clipboard APIs are more reliable than browser `navigator.clipboard` for packaged local app prompt copying.

## Do not promote to memory

Do not promote exact prompt text as canonical marketing copy; it is implementation wording for the local app.

## Follow-up recommendations

Close and relaunch TWB-Marketing from the desktop shortcut before testing Pinterest prompt copy.

Use the next Pinterest run to confirm the prompt now requests a real postable pin asset, not only a written concept.
