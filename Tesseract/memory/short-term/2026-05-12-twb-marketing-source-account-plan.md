# TWB-Marketing Source And Account Planning

## Task

Capture the next planning step for TWB-Marketing after the milestone 1 desktop dashboard: define source/account inventory and decide which platforms can safely feed an opportunity queue.

Scope: shared marketing/account operations for The World Beneath and its World Keys. This is not game development and not auto-posting.

## Result

User clarified the intended app goal:

- Scan approved sources/forums/social surfaces for outreach opportunities.
- Summarize opportunities into a review queue.
- Let the user choose which opportunities to use.
- Provide a `Draft Response` button that calls an LLM only after user action.
- Open a subwindow with the drafted response, a `Copy Response` button, and an `Open Social` button.
- Preserve manual posting by the user.

User account inventory:

- TWB lane accounts already set up: Pinterest, Gmail, Reddit, X, YouTube, itch.io.
- Additional owned/community surfaces confirmed by user: TWB Discord and the TWB website forum.
- Personal accounts already present: LinkedIn, TikTok, Facebook.
- User preference: do not create more personal accounts; any new accounts should be TWB-lane-specific.
- User decision: after reviewing the broader source/community map, stick to the current account/source set for now rather than adding more platforms.

Planning decision:

- Do not treat "scan all my active platforms" as a blanket permission to scrape logged-in feeds, private groups, DMs, or gated communities.
- Treat the safe version as "scan configured public/official sources and approved account surfaces, then queue opportunities for user review."
- Treat TWB Discord announcements and the website forum as owned-community targets to include in the account/source registry. Start with manual copy/open workflows; do not add bot/webhook posting unless separately approved.
- User narrowed the first live opportunity-discovery lane to Reddit and itch.io.
- User wants the first lane to find posts where TWB can be helpful, answer questions, and build notice through usefulness rather than direct game advertising.
- "Forum signature" should be treated as a per-source/per-community rules question, not a blanket pattern. Reddit has no normal forum signature convention, and repeated link/signature text in comments can read as spam/self-promotion. itch.io community rules also restrict advertising/self-promotion unless explicitly specified.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-marketing-source-account-plan.md`

## Checks run

- Read current memory:
  - `memory\hot.md`
  - `memory\index.md`
  - `memory\wiki\game-dev\project-hierarchy.md`
  - `memory\wiki\marketing\_marketing-quickref.md`
  - `memory\wiki\twb-marketing-app\overview.md`
  - `memory\wiki\twb-marketing-app\safety-and-platform-rules.md`
  - `memory\wiki\twb-marketing-app\roadmap.md`
  - `memory\briefs\current-twb-marketing-app-task.md`
- Checked current official/platform documentation signals for Reddit API search, X search API, YouTube Data API search/quota, Gmail API message search, Pinterest API access tiers, itch.io RSS/API, TikTok Display API, and LinkedIn Community Management API.

## Safety boundary confirmation

- No platform connection was added.
- No credentials, tokens, cookies, private account data, or social account settings were requested or stored.
- No scraping, auto-posting, fixed-interval posting, fake engagement, or rule-evasion workflow was created.
- The recommended workflow keeps explicit user review before drafting and explicit user copy/posting before publication.

## Risks

- Platform API access varies widely and changes often.
- "All active social platforms" is not a safe technical target unless each platform/source is named and reviewed.
- Personal LinkedIn/TikTok/Facebook should remain manual-only or be replaced by TWB-lane-specific brand surfaces if the user wants brand activity there.
- LLM drafting requires a separate provider/key decision and local secret-handling plan.

## Memory-worthy notes

- User wants TWB-Marketing to become an opportunity scout and draft assistant, not just a manual dashboard.
- Existing TWB accounts: Pinterest, Gmail, Reddit, X, YouTube, itch.io.
- Existing TWB owned/community surfaces: TWB Discord, including announcements, and TWB website forum.
- Existing personal accounts: LinkedIn, TikTok, Facebook.
- User does not want more personal accounts; any new accounts should be TWB-specific.
- User prefers to stick to the current source/account set for now after reviewing additional community options.
- Safe next product milestone should center on a Source Registry, Account Registry, Opportunity Queue, source scan buttons, LLM drafting on demand, draft review subwindow, copy response, and open-social link.
- First live source priority: Reddit + itch.io only, with a "help-first/no direct ad" response style.
- The Source Registry should include fields for `signatureAllowed`, `linkAllowed`, `promoThreadOnly`, and `helpOnly` so the app can prevent blanket promotional footers.

## Do not promote to memory

- Do not promote any platform API feasibility as final until a platform-specific integration brief reviews the official rules and access requirements.
- Do not promote tentative source examples as approved outreach targets.

## Follow-up recommendations

- Build a local Source Registry and Account Registry before adding any live scanning.
- Start scanning with public/official sources and explicit user-triggered `Scan Now`, not background polling.
- Use Reddit and itch.io as the first proof-of-concept source group.
- Add a response-style guardrail: prioritize genuinely helpful answers; only mention TWB or include a project/community link when the community rules and context allow it.
- Include TWB Discord announcements and the TWB website forum in the registry as manual posting/open-link targets.
- Keep X, YouTube, Gmail, Pinterest, and itch.io as subsequent platform-specific review items.
- Keep personal LinkedIn/TikTok/Facebook out of automated scanning for now; add TWB-specific brand pages/accounts only if the user wants those channels active.
