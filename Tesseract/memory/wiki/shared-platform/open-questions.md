# Shared Platform Open Questions

## Starter Set

- What is the complete starter pet set?
- Is Chuck accepted as the initial DEF starter option?
- Are Peggy, Stanly, and Chuck accepted as final account-creation starter options?
- Which images should be used on the website account-creation cards?
- Should starter pets be grouped into ATK, DEF, and UTIL sections or shown as one grid with role filters?

## Account Flow

- Should the server enforce starter selection inside `/api/auth/register`, or allow account creation then block platform/game access until starter selection is completed?
- Should admin-created accounts bypass starter selection or still require it on first login?
- What support/admin recovery path exists if a player makes a wrong starter choice?

## Inventory

- Which Garden materials become shared transfer items?
- Which Alchemy outputs become shared transfer items?
- Which main-game materials are never shared?
- Should companion levels/cooldowns be global, per-game, or split between global identity and per-game projection?
- How does The Garden earn or receive `glassroot_garden_token` for pet purchases?

## Deployment

- Should `0020_admin_support_tickets.sql` be approved for remote D1 migration after manual local admin-session testing?
- Should BobNet retirement production cleanup proceed now, including remote D1 migrations `0015` and `0016`?
- Should the live Cloudflare secret `BOB_FORGE_ADMIN_PASSWORD` be deleted after the Worker no longer uses Bob/BobNet package-hub code?
- Is a served Wrangler dev preview required before the live cleanup gate, given the prior local smoke attempt timed out?
- What live verification checklist should be required after deploying the cleanup?
- What backend event contract, idempotency model, lock lifetime policy, and conflict resolution should govern the eventual shared companion mutation path?

## Admin Support

- Which games should get the first Report Bug button: Garden, Alchemy, Trenchworks, main Unity, or website-only first?
- What rate limiting / abuse-control rule should protect public `POST /api/support/tickets`?
- Which email provider, unsubscribe model, and consent language should be used before any real customer emailing is added?
- Should moderators eventually see support tickets, or should ticket/PII access remain admin-only?

## Creator Commercial Licensing

- Should the Tier 2 trigger be `$100,000` in TWB-attributable covered gross revenue over a trailing 12-month period?
- Is `2%` above the first `$100,000` the right starting royalty candidate?
- Should Tier 1 subscription fees credit against Tier 2 royalties?
- What exact rights does the `$20/month` Creator Access tier grant?
- What counts as a TWB-derived commercial product or service?
- Should store/platform fees be excluded from covered gross revenue, or only refunds/chargebacks and collected/remitted taxes?
- Should Tier 2 be automatic after threshold crossing or require manual commercial-license review?
- What legal/accounting review is needed before public Kickstarter copy mentions creator commercialization?

## Sources

- User requirement on 2026-05-12
- Website/source inspection, 2026-05-12
- [[short-term/2026-05-13-twb-unity-starter-pets-worker-final-decommission-report]]
- [[short-term/2026-05-13-twb-shared-platform-bobnet-removal-final-decommission-report]]
