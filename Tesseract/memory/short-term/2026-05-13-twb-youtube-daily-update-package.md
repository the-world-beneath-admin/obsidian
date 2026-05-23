# TWB YouTube Daily Update Package - 2026-05-13

## Task

Create today's The World Beneath daily update package for TWB YouTube using confirmed Obsidian memory and existing video/trailer hook material first.

Scope: The World Beneath parent/main game, with World Keys framed as playable subgame/module lanes.

## Result

Created a HyperFrames-based 32-second caption-led YouTube video package at:

`C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13`

Rendered video:

`C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\renders\twb-daily-youtube-2026-05-13.mp4`

Rendered video with selected audio:

`C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\renders\twb-daily-youtube-2026-05-13-with-audio.mp4`

The package includes title, description, tags, pinned comment, thumbnail idea, memory grounding, short script, shot list, asset/video checklist, audio selection notes, and manual posting checklist.

Correction after review: the first render used internal framing language such as "approved pitch" and process/guardrail notes in the visible video. The composition was revised into a truly public-facing asset with only viewer-facing copy. Source-grounding notes were moved out of the upload package into a separate internal file.

## Files touched

- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\DESIGN.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\index.html`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\narration.txt`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\youtube-package.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\audio-selection.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\internal-source-grounding.md`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\package.json`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\package-lock.json`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\assets\*`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\assets\twb-daily-music-bed.mp3`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\renders\twb-daily-youtube-2026-05-13.mp4`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\renders\twb-daily-youtube-2026-05-13-with-audio.mp4`
- `C:\Users\yrred\Desktop\Markeing\TWB-Marketing\outputs\youtube-daily-2026-05-13\renders\twb-daily-youtube-2026-05-13-contact-sheet.jpg`

## Checks run

- `npx hyperframes doctor`
  - HyperFrames 0.6.4, Node, and Chrome were available.
  - FFmpeg/FFprobe were not on PATH, so local npm dev dependencies were installed for rendering.
- `npx hyperframes lint`
  - Passed with one maintainability warning: `timeline_track_too_dense`.
- `npx hyperframes validate`
  - Passed. No browser console errors; text elements met WCAG AA contrast.
- `npx hyperframes inspect --samples 16`
  - Passed after marking the transition bar as intentionally overflowing.
- `npx hyperframes render --output renders/twb-daily-youtube-2026-05-13.mp4 --quality standard`
  - Render succeeded.
- Local `ffprobe`
  - Confirmed MP4 is 1920x1080, 30fps, 32.000 seconds, 4,314,385 bytes.
- Local `ffprobe`
  - Confirmed the audio version has one H.264 video stream, one AAC audio stream, and is 32.000 seconds.
- Local `ffmpeg`
  - Created contact sheet for visual QA.
- Local `ffmpeg`
  - Added selected `twb-day2.mp3` audio as a trimmed, faded, normalized 32-second music bed.
- `rg`
  - Confirmed the public-facing source files no longer contain the internal/process phrases that made the first render unsuitable for posting.

## Cleanup performed

Removed the generated `node_modules` folder from the package after rendering and verification. `package.json` and `package-lock.json` remain so dependencies can be restored with `npm install` if the video needs re-rendering.

Retained the MP4 and contact sheet because they are final package artifacts, not throwaway screenshots.

## Safety boundary confirmation

No auto-posting was built or performed.

No platform API connection, social login, account connection, scraping, fake engagement, rule evasion, or external notification integration was added.

The YouTube upload is manual only. The package includes a manual posting checklist.

The corrected video does not claim the full main game is live. World Keys are described as smaller playable lanes/module corners while the full game grows.

The selected audio was local project/user audio only; no external music API, platform API, or auto-upload workflow was used.

## Risks

The rendered video is caption-led and silent. A narration script exists, but HyperFrames TTS could not run because local Python packages `kokoro-onnx` and `soundfile` are not installed.

The first render demonstrated a process risk: source-grounding language must never be placed directly into public-facing scenes. The corrected package separates public upload copy from internal grounding notes.

Audio choice was made from existing local tracks. `twb-day2.mp3` was selected because it is TWB-labeled and long enough for a clean 32-second music bed.

## Memory-worthy notes

The first tested daily YouTube package angle is clarity-first: explain what players do in The World Beneath before introducing the larger shared-world frame.

The package uses the confirmed approved copy: "Run dungeons. Grow creatures. Shape the world beneath."

The first named World Keys used in public-facing framing are The Garden and The Alchemy Lab.

For future daily video generation, install or configure the local HyperFrames TTS requirements if narrated videos are desired.

For future daily video generation, prefer TWB-labeled marketing tracks first, then use Unity music tracks only when the video needs stronger lore or in-game atmosphere.

## Do not promote to memory

Do not promote the exact daily script as permanent canonical copy; it is a one-day content draft.

Do not promote the temporary HyperFrames project layout as a required long-term pipeline until the process is tested with more daily queue items.

## Follow-up recommendations

Review the silent/caption-led MP4 manually before upload.

If voiceover is desired, install `kokoro-onnx` and `soundfile`, regenerate narration audio, and re-render.

After uploading to TWB YouTube, mark the daily queue item as posted in the dashboard.

Test one more daily queue item for Pinterest or LinkedIn next so the queue can prove both video and non-video workflows.
