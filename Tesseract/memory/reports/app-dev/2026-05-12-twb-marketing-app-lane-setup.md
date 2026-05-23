# App Dev Report - 2026-05-12 - TWB-Marketing App Lane Setup

## Task

Define a new TWB-Marketing app lane, create the first permanent memory notes, prepare the first bounded app-dev task brief, and document the safety boundary for forum/social workflows.

## Result

Created a new permanent memory lane for TWB-Marketing as a local-first marketing operations app. The lane defines scope, safety rules, roadmap, first coding milestone, recommended specialist role, and the first active task brief.

## Files Touched

- `memory/wiki/twb-marketing-app/overview.md`
- `memory/wiki/twb-marketing-app/safety-and-platform-rules.md`
- `memory/wiki/twb-marketing-app/roadmap.md`
- `memory/briefs/current-twb-marketing-app-task.md`
- `memory/reports/app-dev/2026-05-12-twb-marketing-app-lane-setup.md`
- `memory/wiki/memory/multi-agent-orchestration-system.md`
- `memory/index.md`
- `memory/hot.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\app-dev.toml`
- `C:\Users\yrred\Documents\New project 2\.codex\agents\orchestrator.toml`

## Checks Run

- Read required memory rules, hot file, index, multi-agent system, and project hierarchy.
- Confirmed existing briefs, wiki folders, reports folders, templates, and custom agents.
- No app code was created or tested.

## Memory-Worthy Notes

- Fact - TWB-Marketing is a shared marketing operations app lane for The World Beneath and its World Keys.
- Decision - Start with a small local app foundation rather than full marketing automation.
- Decision - The app may assist with drafting, scheduling plans, tracking, and review.
- Decision - The app must not auto-post, connect social accounts, scrape private data, spam, fake engagement, or evade platform rules.
- Decision - Use `app-dev` as the recommended specialist for bounded app implementation.
- Decision - Defer `social-ops` until platform rules and safe manual workflows are reviewed.

## Do Not Promote To Memory

- Specific UI layout choices beyond the first milestone recommendation.
- Any future API or posting integration ideas.
- Any assumptions about platform-specific rules not yet reviewed from official sources.

## Next Worker Should Do

Use the `app-dev` role and read `memory/briefs/current-twb-marketing-app-task.md` first. Create a local-only Vite + React + TypeScript app foundation under `C:\Users\yrred\Documents\New project 2\twb-marketing-app`, using seed/mock data and no external integrations. Build a usable internal operations dashboard and run `npm run build`.

## Risks

- Scope creep into social automation must be resisted.
- Platform rules are not yet reviewed, so integrations remain blocked.
- The first app milestone should avoid overbuilding storage, auth, analytics, or scheduling infrastructure.

