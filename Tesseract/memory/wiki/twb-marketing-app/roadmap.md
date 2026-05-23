# TWB-Marketing App Roadmap

## Status

Initial roadmap - created 2026-05-12.

## First Coding Milestone

Build a small local app foundation that can run without external accounts, APIs, or posting permissions.

After the user clarified the desired agentic direction, the first milestone should be narrowed to a safe **opportunity-discovery and draft-review assistant**. It should help find public opportunities and prepare reviewed responses, but it must not post automatically.

Recommended stack for the first worker:

- Vite
- React
- TypeScript
- Local seed data or browser storage only

Recommended first screen:

- Campaign overview
- Draft queue
- Platform readiness checklist
- Asset/copy bank preview
- Approval status indicators
- Opportunity/rule-risk review queue
- Alert center with quiet-hours / sleep-mode controls

## First Milestone Status

Milestone 1 is complete and decommissioned (reviewed 2026-05-13):

- Delivered a local Electron + Vite + React dashboard foundation.
- The currently verified executable path is `C:\Users\yrred\Desktop\Marketing\TWB-Marketing\release\win-unpacked\TWB-Marketing.exe`.
- Blank packaged-window behavior was fixed by using `base: './'` in `vite.config.ts`.
- No external API, account, posting, fixed-interval, or automatic alert channel integration exists in milestone 1.
- A working Scout prototype now exists for public Reddit and itch.io discovery with manual-review draft flow only.
- The current app surface is Overview, Scout, Marketing, Daily Queue, Passwords, and Archive.
- Daily Queue now tracks manual platform packages with explicit posting states and a manual posted confirmation flow.
- The Garden itch.io lane is held until The Garden World Key is release-ready.

## First Milestone Done Criteria

- Local app scaffold exists under the orchestration workspace.
- The app shows a usable marketing operations dashboard, not a landing page.
- Data is local-only and mock/seeded.
- No social/forum/store APIs are installed or called.
- No credentials, tokens, or account connections are requested.
- No fixed-interval posting or posting automation exists.
- Every drafted response remains manual-review only.
- Alerting is represented as local app state only: importance tiers, quiet-hours settings, alert-mute mode, high-importance-only sleep throttle, queued alerts, snooze/mute controls, and digest-after-quiet-hours behavior.
- No external push-notification, email, SMS, or OS-level notification integration is required for the first milestone unless separately approved.
- Build check passes.
- Milestone report is written under `memory/short-term/` and reviewed by the curation automation.

## Later Modules

- Campaign calendar with campaign phases and deadlines.
- Drafting queue for forum posts, social posts, store updates, newsletters, and creator outreach.
- Forum outreach tracker with community rules, fit, status, and last-contact notes.
- Social platform checklist with account readiness and manual posting requirements.
- Asset/copy bank for approved text, screenshots, capsules, trailers, logos, and tags.
- Approval workflow with draft, review, approved, posted, and archived states.
- Alerting and quiet-hours system for high-importance opportunities, queued digests, snooze, mute, and wake-time reminders.
- Analytics/import notes after official export or integration rules are reviewed.

## Next Coding Milestone

If app development resumes, the next useful local-only pass is a status-history export/import feature for Daily Queue records. Keep all posting manual.

Do not add:

- schedulers
- auto-posting
- platform APIs
- account connections
- scraping
- external notifications

## OpenAI Developer Tooling Note

- Fact - Codex plan usage can help build and modify code through Codex sessions.
- Decision - A runtime agent that calls OpenAI models should use OpenAI API access through a reviewed API-key setup, not assume Codex plan analytics are a general-purpose bot runtime.
- Warning - Do not design the presence agent around unverified assumptions that ChatGPT/Codex OAuth usage can power autonomous background posting.
- Source: OpenAI Codex and API documentation checked 2026-05-12.

## Memory Artifacts Needed

- Wiki lane: `memory/wiki/twb-marketing-app/`
- Active brief: `memory/briefs/current-twb-marketing-app-task.md`
- App-dev reports: `memory/reports/app-dev/`
- Future raw evidence, only if needed: `memory/raw/marketing-app/`

## Specialist Recommendation

- Decision - Add `app-dev` as the recommended specialist role for bounded TWB-Marketing app implementation, debugging, tests, and reports.
- Decision - Do not add `social-ops` as an active worker yet. Use launch/marketing specialists for platform-rules research first; consider `social-ops` only after safe manual workflows are established.
- Warning - A social-ops role must never be scoped to spam, fake engagement, or rule evasion.
- Source: User request, 2026-05-12.
