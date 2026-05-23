# Current TWB-Marketing App Task

## Goal

Implement the next safe local TWB-Marketing milestone: Daily Queue and manual posting-state control.

## Scope

Shared marketing operations app for The World Beneath and its World Keys.

This is not the main game, not a World Key, and not a social automation or auto-posting project.

## Read First

1. [[wiki/twb-marketing-app/overview]]
2. [[wiki/twb-marketing-app/safety-and-platform-rules]]
3. [[wiki/twb-marketing-app/roadmap]]
4. [[wiki/twb-marketing-app/alerting-and-quiet-hours]]
5. [[wiki/game-dev/project-hierarchy]]
6. [[wiki/marketing/_marketing-quickref]]
7. [[wiki/launch/world-keys-itch-io-release-briefs]]
8. [[short-term/2026-05-13-twb-marketing-worker-final-decommission-report]]
9. [[short-term/2026-05-13-twb-marketing-daily-prompt-audit]]
10. [[short-term/2026-05-13-twb-itchio-world-key-devlog-package]]

## Recommended Specialist

Use an `app-dev` worker for the next coding pass.

## Allowed Write Paths

- `C:\Users\yrred\Desktop\Marketing\TWB-Marketing\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\`

## Forbidden Write Paths

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\wiki\`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\index.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\hot.md`
- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\log.md`
- Any social, forum, store, or community account settings.
- Any credentials, tokens, cookies, or private account data.

## Constraints

- Make the smallest useful local app foundation.
- Do not connect APIs.
- Do not create auto-posting.
- Do not create fixed-interval posting.
- Do not create account login.
- Do not scrape private or gated data.
- Do not build spam, disguised advertising, fake engagement, hashtag evasion, or rule-evasion features.
- Preserve a manual approval concept for any drafted post.
- Include a local alert/quiet-hours concept so alerts can be muted while the user sleeps, the system can optionally throttle gathering to high-importance-only during sleep, and queued reminders can be reviewed later.
- Do not add external push notification, email, SMS, or OS-level notification integrations unless separately approved.
- Do not add OpenAI API calls in this milestone.
- Do not add social platform SDKs, scraping libraries, or automation libraries in this milestone.
- Use local seed data or local browser storage only.
- Write relevant implementation notes, risks, and memory-worthy findings to an Obsidian report under `memory/short-term/`; do not update permanent wiki memory directly.
- Clean up temporary files, scratch files, generated screenshots, throwaway logs, and dev artifacts created during the task when they are no longer needed. Do not delete source files, user files, raw evidence, reports, or another worker's work.

## First Coding Milestone Recommendation

Milestone 1 is complete and decommissioned.

## Next Coding Milestone Recommendation

Implement a Daily Queue status pass in the existing Electron + Vite + React + TypeScript local app at:

```text
C:\Users\yrred\Desktop\Marketing\TWB-Marketing
```

The pass should add:

- local-only queue statuses such as Ready, Needs Asset, Blocked, Held, and Posted
- an explicit Held state for itch.io / The Garden until The Garden World Key is release-ready
- manual "Mark posted" confirmation flow
- posted date/state in local Daily Queue data
- output-folder or reference fields where they fit existing data patterns
- per-platform notes explaining why a lane is ready, blocked, or held

## Done When

1. Daily Queue shows and stores explicit status per lane.
2. The Garden / itch.io lane is visibly Held until The Garden is release-ready.
3. Posted state can only be set manually with confirmation.
4. The workflow does not add schedulers, platform APIs, scraping, account connections, auto-posting, or external notifications.
5. Password vault behavior is untouched unless directly necessary.
6. `npm run build` passes.
7. `npm test` passes.
8. `npm run package:win` is run if source changes affect the desktop executable.
9. The worker writes a report to `memory/short-term/`, preferably `2026-05-13-twb-marketing-daily-queue-status-pass.md`.

## Report Required

Return:

1. Task
2. Result
3. Files touched
4. Checks run
5. Risks
6. Safety boundary confirmation
7. Memory-worthy notes
8. Do not promote to memory
9. Follow-up recommendations
