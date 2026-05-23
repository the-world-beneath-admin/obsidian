# Creator Commercial License Structure

## Status

Draft internal structure recorded on 2026-05-22. This is not legal advice and is not final public legal/policy copy.

## Purpose

The creator platform should let small creators participate without fear while still protecting Bob/The World Beneath if a creator or company materially profits from TWB-derived commercial work.

The structure should avoid vague "profit share" language. Use covered gross revenue / royalty / commercial license language instead.

## Research Signals

- Unreal Engine uses a gross-revenue royalty model: royalties apply after a large revenue threshold and are based on revenue directly attributable to the product.
- Creative Commons warns that NonCommercial is flexible and intent-based, so TWB should not rely on a generic NC framing for commercial creator enforcement.
- Kickstarter says creators keep ownership of their work and projects cannot offer equity, financial returns, or loans; Kickstarter creator rewards should not promise backers a share of future creator-platform revenue.
- Stripe Tax / Connect documentation emphasizes determining which party is responsible for tax collection/reporting before implementing marketplace or platform payments.

## Recommended Structure

### Tier 0 - Community / Noncommercial

For fans, community discussion, feedback, personal play, noncommercial fan expression, and ordinary community participation.

Rules:

- No paid subscription required.
- No right to sell TWB-derived products, paid modules, paid tools, or commercial services.
- No formal submission/review expectation unless a separate submission path opens.
- No canon, partnership, compensation, or adoption promise.

### Tier 1 - Creator Access

Price:

- `$20/month`.

Purpose:

- A low-friction creator-platform subscription for hobbyists, testers, early creators, and small commercial experiments.

Suggested rights:

- Access to creator tools, documentation, private drafts, templates, and approved creator resources.
- Permission to build and test TWB-compatible creator materials under the creator terms.
- Limited commercial permission only while below the commercial threshold.

Suggested limits:

- Applies only while the creator remains below `$100,000` in covered gross revenue over a trailing 12-month period.
- No sublicensing of TWB IP.
- No implying official canon, official partnership, or endorsement unless separately approved.
- No use of TWB trademarks/logos beyond approved attribution badges and marketplace labels.

### Tier 2 - Commercial Creator License

Trigger:

- Required when a creator, company, or affiliated entity crosses `$100,000` in covered gross revenue over a trailing 12-month period from TWB-derived commercial products or services.

Recommended definition:

- Covered gross revenue means all gross receipts directly attributable to TWB-derived commercial products or services, before salaries, contractors, operating expenses, ad spend, and general business costs.

Recommended exclusions to consider:

- Refunds, chargebacks, and cancelled transactions.
- Sales tax / VAT / GST collected and remitted.
- Unrelated company revenue that is not attributable to TWB-derived products or services.

Do not exclude by default without review:

- Store/platform fees.
- Payment processing fees.
- Marketing costs.
- Contractor payments.
- Owner salary.

Payment model:

- Tier 2 keeps the `$20/month` platform subscription or replaces it with a commercial account fee, pending billing design.
- Revenue-share/royalty recommendation: `2%` of covered gross revenue above the first `$100,000` per trailing 12-month period.
- Payments should be reported and paid quarterly.
- Tier 1 subscription fees paid during the same period may be credited against the royalty due if Bob wants the system to feel less punitive.

High-success review:

- If covered gross revenue exceeds `$1,000,000` in a trailing 12-month period, the creator should move to a custom commercial license review.
- Default fallback until custom terms are signed: the Tier 2 royalty continues.

## Reporting And Verification

Minimum reporting cadence:

- Quarterly self-report covering covered gross revenue, refunds/chargebacks, taxes collected/remitted, products/services sold, and payment due.

Suggested records:

- Store payout reports.
- Stripe/PayPal/payment processor reports.
- Marketplace dashboards.
- Sales summaries by product.

Audit right:

- TWB should reserve the right to request supporting records for a defined lookback period, such as `3` or `4` years.

Transition window:

- Creator must notify TWB within `30` days of crossing the Tier 2 threshold.
- Creator has `60` days from crossing to complete Tier 2 setup unless a different written agreement is made.

## Kickstarter Boundary

Do not frame creator-platform backer rewards as investment, equity, passive income, revenue share, loans, or financial returns.

Safer Kickstarter framing:

- Access to creator tools when available.
- Founder/early creator subscription months.
- Private development updates.
- Credits, badges, or community recognition.
- Noncommercial/early creator experiments subject to final creator terms.

Avoid promising:

- Backers receive a share of future creator-platform revenue.
- Backers own part of TWB.
- Backers get guaranteed business opportunity, income, or marketplace success.

## Account / Admin Fields Needed Later

Potential account fields:

- `creator_tier`: `none`, `community`, `tier1`, `tier2`, `enterprise`
- `creator_status`: `inactive`, `active`, `pending_review`, `suspended`
- `creator_terms_version`
- `creator_terms_accepted_at`
- `covered_revenue_threshold_usd`
- `tier2_started_at`
- `next_revenue_report_due_at`
- `last_revenue_report_at`
- `commercial_license_notes`

Potential tables:

- `creator_accounts`
- `creator_revenue_reports`
- `creator_license_events`
- `creator_terms_versions`

## Public Copy Direction

Short safe public wording:

> The creator platform is planned to support small creators with a low monthly access tier and a separate commercial license for larger companies or high-earning creator businesses. Formal creator submissions and commercial licensing are not open yet. Final terms will be published before creators are asked to rely on them.

Policy wording should be lawyer-reviewed before launch:

> Tier 1 Creator Access is intended for small creators and early commercial experiments. If your TWB-derived creator products or services exceed the commercial revenue threshold, you must move to the Commercial Creator License and report covered gross revenue on the required schedule.

## Decisions To Make Before Implementation

- Confirm whether the threshold is exactly `$100,000` in covered TWB-attributable gross revenue.
- Confirm whether `2%` above the threshold is the starting percentage.
- Decide whether Tier 1 monthly fees credit against Tier 2 royalties.
- Decide whether Tier 2 is automatic or manually reviewed before activation.
- Decide what creator rights Tier 1 actually grants.
- Decide what counts as a TWB-derived commercial product.
- Decide whether creator payments are handled through Stripe subscriptions, Stripe invoicing, marketplace payments, or manual agreements first.
- Have counsel review the public creator policy, terms, audit language, IP license language, and revenue definitions.

## Sources

- Epic / Unreal Engine licensing page, checked 2026-05-22.
- Creative Commons NonCommercial interpretation, checked 2026-05-22.
- Kickstarter support guidance on backer rewards and ownership, checked 2026-05-22.
- Stripe Tax / Connect documentation, checked 2026-05-22.
