# App Dev Report - 2026-05-12 - Agentic Presence Safety Scope Correction

## Task

Clarify the user's intended TWB-Marketing goal as an agentic online presence system, reject unsafe automation requirements, and prepare a safe worktree and subagent hydration prompt.

## Result

Created a safe planning worktree for a TWB Marketing Presence Agent and updated the Obsidian app lane to focus the first milestone on opportunity discovery, rule-risk review, draft assistance, disclosure support, and approval queueing.

The unsafe requested capabilities remain blocked:

- fixed-interval posting, such as one post every 10 minutes
- disguised advertising
- evading no-advertising or self-promotion rules
- auto-posting to forums, Reddit, itch.io, X/Twitter, Discord, Steam, or other communities
- fake engagement, sockpuppeting, fake votes, fake replies, or synthetic community activity
- private/gated/logged-in scraping

## Files Touched

- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\README.md`
- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\SUBAGENT_HYDRATION_PROMPT.md`
- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\docs\safe-agent-contract.md`
- `memory/wiki/twb-marketing-app/safety-and-platform-rules.md`
- `memory/wiki/twb-marketing-app/roadmap.md`
- `memory/briefs/current-twb-marketing-app-task.md`
- `memory/reports/app-dev/2026-05-12-agentic-presence-safety-scope-correction.md`
- `memory/index.md`
- `memory/hot.md`
- `memory/log.md`

## Checks Run

- Read `memory/hot.md`, `memory/index.md`, `memory/wiki/memory/multi-agent-orchestration-system.md`, `memory/wiki/game-dev/project-hierarchy.md`, and the TWB-Marketing safety note.
- Checked OpenAI official Codex/API documentation to clarify that Codex usage is for Codex coding tasks, while API-backed runtime apps use OpenAI API keys.
- No executable app code was created.

## Safety Boundary Confirmation

No auto-posting, fixed-interval posting, account connections, credentials, private scraping, or rule-evasion features were created.

## Memory-Worthy Notes

- Fact - The user wants an agentic online presence system for The World Beneath marketing.
- Decision - The safe version is an opportunity-discovery and draft-review assistant, not an automated posting bot.
- Decision - Any response must remain queued for explicit user approval before posting.
- Warning - Fixed-interval posting, disguised advertising, fake engagement, and rule evasion are blocked.
- Warning - Codex plan analytics should not be treated as a general-purpose autonomous posting runtime.

## Do Not Promote To Memory

- Any plan to post every 10 minutes.
- Any platform-specific integration details before official rules are reviewed.
- Any assumption that a platform allows automated posting.

## Follow-Up Recommendations

1. Decide whether milestone 1 should be a local dashboard or a CLI/report generator.
2. Review official rules for the first target platform before any integration.
3. If using OpenAI model calls, complete the OpenAI API-key setup gate before writing API-backed agent code.
4. Use the hydration prompt in `twb-marketing-presence-agent\SUBAGENT_HYDRATION_PROMPT.md` for a bounded app-dev worker.
