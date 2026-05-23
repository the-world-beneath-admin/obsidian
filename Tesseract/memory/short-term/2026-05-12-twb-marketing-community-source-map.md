# TWB-Marketing Community Source Map

## Task

Identify additional game development, AI development, and general community sources to account for before moving the TWB-Marketing app from manual dashboard toward opportunity scanning and draft response workflows.

Scope: shared TWB / World Keys marketing-account operations. This is not game development, not auto-posting, and not social account automation.

## Result

Recommended source categories to account for:

- Core player and store communities: Reddit, itch.io, Steam Community/Discussions once Steam page exists, YouTube, X, Bluesky, Mastodon/ActivityPub, Pinterest.
- Indie/game-dev communities: GameDev.net, TIGSource, IndieDB, Game Jolt, selected Discord communities, selected subreddit communities, Game Development Stack Exchange.
- AI/dev communities: OpenAI Developer Community, Hugging Face Forums, selected Reddit AI communities, possibly Hacker News/Indie Hackers as read-only signal sources.
- Owned/community surfaces: TWB website/news, Gmail inbox, future mailing list, future TWB Discord server if the user wants an owned community hub.
- Creator/press sources: YouTube/TikTok creator search, press/blog/RSS feeds, curator lists, and manual lead lists.

Recommended priority:

1. Build Source Registry and Account Registry in the app.
2. Start with public/read-only or official-access sources that can generate opportunity summaries without account-risk: Reddit configured communities, itch.io feeds/pages, selected public forums/RSS.
3. Add "Open Social" links and manual posting only.
4. Defer Discord, personal Facebook/TikTok/LinkedIn, and any gated communities until specific TWB-lane accounts/surfaces and rules are defined.

Update after user review:

- User confirmed TWB already has a Discord.
- User wants TWB Discord announcements included as a posting lane and wants the app to help drive people toward the community.
- User confirmed the TWB website has a forum.
- User wants to stick to the currently identified account/source set rather than add more communities for now.
- Revised recommendation: include TWB Discord announcements and the TWB website forum in the registry from the next app milestone, but treat them as owned manual posting/open-link targets first. Do not add Discord bot/webhook posting unless separately approved.

## Files touched

- `C:\Users\yrred\Desktop\Obsidian\Tesseract\memory\short-term\2026-05-12-twb-marketing-community-source-map.md`

## Checks run

Reviewed current public/platform docs and community pages for:

- Steam Community/Steamworks hub/discussions behavior.
- Bluesky API documentation.
- Mastodon search API.
- Discord Gateway and privileged intent restrictions.
- GameDev.net community positioning.
- TIGSource forums.
- Stack Exchange API.
- IndieDB promotional/community profile tooling.
- Hugging Face Forums.
- OpenAI Developer Community.

## Safety boundary confirmation

- No credentials, tokens, cookies, or private account data were accessed.
- No social or platform integrations were added.
- No scraping or posting automation was created.
- Recommendations preserve manual review, copy, and user posting.

## Risks

- Discord and many social communities are gated or require privileged access for message content; they should not be scanned without explicit account/server permission and rule review.
- TWB Discord is confirmed as an owned surface, but bot/webhook posting still needs a separate explicit integration decision if the user wants more than copy/open-link support.
- Stack Exchange and developer forums are poor places for promotion; use only for genuine technical questions/answers or read-only signal.
- AI developer communities may be relevant for devlog/tooling posts, but not primary game marketing unless the content is genuinely about AI/game-development tooling.
- Bluesky and Mastodon are promising public-social scan candidates, but both need platform-specific source/query rules.

## Memory-worthy notes

- Additional source classes should be accounted for before implementation: Steam Community, Bluesky, Mastodon, Discord, GameDev.net, TIGSource, IndieDB, Game Jolt, Stack Exchange, OpenAI Developer Community, Hugging Face Forums, and creator/press RSS/search sources.
- Recommended implementation is a registry-first model, not hard-coded platforms.
- Personal Facebook/TikTok/LinkedIn should remain manual-only unless TWB-specific brand accounts/pages are created.
- User has chosen to stick with the current practical source/account set for now, with TWB Discord and TWB website forum added as owned-community surfaces.

## Do not promote to memory

- Do not treat every listed community as an approved posting target.
- Do not treat "AI community" as a primary marketing lane without a specific TWB AI/devtool angle.
- Do not promote any platform API feasibility as final until a platform-specific integration brief reviews official terms and access limits.

## Follow-up recommendations

- Add Source Registry fields: platform, source URL/query, TWB/personal account lane, access method, scan mode, posting mode, rule status, blocked terms, allowed response style.
- Add Account Registry fields: account type, platform, handle/profile URL, owner, status, posting mode, open-link URL, notes.
- Use a first proof-of-concept with Reddit + itch.io/public RSS or public forums before adding API-heavy platforms.
- Add owned-community fields for Discord announcements and website forum links so approved drafts can include `Copy Response` and `Open Social` without auto-posting.
