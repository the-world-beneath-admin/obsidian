# TWB-Marketing Alerting And Quiet Hours

## Status

Active product requirement - created 2026-05-12.

## Purpose

The presence agent must remind the user about worthwhile opportunities without becoming a constant interruption system.

## Core Model

- The agent may gather opportunities continuously or on a schedule.
- Alerts must respect quiet hours / sleep mode.
- Quiet hours should support two modes:
  - Alert mute - keep gathering opportunities, but queue normal and low-importance items silently.
  - Sleep throttle - gather only high-importance opportunities until quiet hours end.
- During quiet hours, only high-importance opportunities may interrupt the user.
- When quiet hours end, the system should send a digest or reminder after a configurable delay.
- The user must be able to mute alerts or mute the whole system temporarily.

## Importance Tiers

- Low - informational, weak fit, no urgency.
- Normal - relevant opportunity, no short deadline.
- High - time-sensitive, strong fit, or likely to materially affect launch/marketing if missed.
- Blocked - unsafe, rule-risky, irrelevant, promotional where promotion is forbidden, or needs human decision before any action.

## Default Behavior Recommendation

- Quiet hours enabled by default.
- High-importance interruption during quiet hours disabled until the user explicitly enables it.
- Digest after quiet hours enabled by default.
- Snooze/mute controls visible in the app.
- Every alert links to the opportunity, rule-risk notes, recommended action, and draft/review status.

## Safety Rules

- Alerts must never imply the app has posted or will post automatically.
- Alerts should be about review opportunities, not pressure to spam.
- High-importance criteria must stay conservative.
- If a platform or community rule blocks promotional engagement, the alert should mark the opportunity as blocked or review-only.

## Memory Items

- Decision - Alerting and quiet-hours controls are a core TWB-Marketing app requirement.
- Decision - The app should support sleep/quiet mode, alert mute, high-importance-only sleep throttle, queued opportunities, and wake/digest reminders.
- Warning - Do not tune alerting to maximize posting volume. Tune it to protect attention and surface genuinely important review items.
- Source: User clarification, 2026-05-12.
