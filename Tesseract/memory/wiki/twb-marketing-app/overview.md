# TWB-Marketing App Overview

## Status

Active app lane - created 2026-05-12; first worker decommission reviewed 2026-05-13.

## Scope

TWB-Marketing is a local-first marketing operations app for **The World Beneath** and its World Key subgames.

## Memory Items

- Fact - The app lane supports marketing work for The World Beneath, The Garden, The Alchemy Lab, and future World Keys.
- Decision - The app should begin as a small local tool, not a connected posting system.
- Decision - The app should assist with campaign planning, draft preparation, readiness tracking, asset/copy organization, and approval review.
- Decision - The app must not auto-post, fake engagement, spam communities, evade platform rules, scrape private data, or connect social accounts until platform rules and account permissions are reviewed.
- Fact - Milestone 1 is implemented as a local Electron + Vite + React desktop application at `C:\Users\yrred\Desktop\Marketing\TWB-Marketing`.
- Fact - The currently verified executable path is `C:\Users\yrred\Desktop\Marketing\TWB-Marketing\release\win-unpacked\TWB-Marketing.exe`.
- Fact - Milestone 1 data remains local/manual and the executable contains no backend auth database, platform API, posting automation, or social-account connection path.
- Fact - The current main navigation is Overview, Scout, Marketing, Daily Queue, Passwords, and Archive.
- Fact - A Scout prototype now scans public Reddit and itch.io surfaces, queues helpful-reply opportunities, and keeps draft response review manual.
- Fact - The Marketing tab holds direct-promotion lanes only; `r/indiegames` belongs there rather than in Scout.
- Fact - The Daily Queue tab is local/manual only; it copies Bob/Codex prompts for platform update packages and does not auto-post. Daily Queue now covers YouTube, Pinterest, Discord, X, LinkedIn, Facebook, TikTok, and held itch.io draft lanes.
- Fact - Daily Queue now has explicit local posting states: Ready, Needs Asset, Blocked, Held, and Posted.
- Fact - Daily Queue uses a manual Mark posted confirmation dialog, records `lastPostedAt` locally, and carries output-folder, reference, and status-note fields for each lane.
- Fact - The Passwords tab exists as a local Windows-encrypted personal password vault for this PC.
- Fact - Local Gemma drafting was chosen for draft assistance after the user rejected using Codex OAuth/OpenAI as the runtime for this feature.
- Decision - itch.io posting for The Garden is held until The Garden World Key is release-ready.
- Warning - The current executable is an unsigned local/unpacked build, so distribution should stay internal for now.
- Warning - The app directory is not currently a git repository, so there is no local git diff/commit trail inside `C:\Users\yrred\Desktop\Marketing\TWB-Marketing`.
- Warning - The password vault is personal/local only and has not had a formal security audit, backup plan, or recovery plan.
- Decision - Future app milestones should preserve the same local-first review model unless a platform-safe approval workflow is approved.
- Warning - Treat forum and social workflows as reviewed, user-approved operations. Do not build hidden automation or engagement manipulation.
- Source: User request, 2026-05-12.
- Source: [[short-term/2026-05-13-twb-marketing-worker-final-decommission-report]]

## Intended Modules

- Campaign calendar
- Post drafting queue
- Forum outreach tracker
- Social platform checklist
- Asset/copy bank
- Approval workflow before posting
- Analytics/import notes later

## Current Boundary

The first goal is now complete: local-only, review-focused desktop dashboard milestone is delivered and decommissioned while preserving safe-agent boundaries.

The Daily Queue and posting-state control pass is complete. The next gate is visual confirmation of the packaged app and, if app work resumes later, a local export/import pass for status history.
