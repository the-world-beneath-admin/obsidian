# App Dev Report - 2026-05-12 - Alerting And Quiet Hours Requirement

## Task

Add alerting, sleep/quiet-hours muting, high-importance opportunity handling, and queued reminder behavior to the TWB-Marketing presence-agent lane.

## Result

Alerting is now treated as a core product requirement. The first app milestone should visibly model notification preferences, importance tiers, quiet hours, alert-mute mode, high-importance-only sleep throttle, queued reminders, snooze/mute controls, and digest/reminder behavior after quiet hours.

## Files Touched

- `memory/wiki/twb-marketing-app/alerting-and-quiet-hours.md`
- `memory/wiki/twb-marketing-app/roadmap.md`
- `memory/briefs/current-twb-marketing-app-task.md`
- `memory/index.md`
- `memory/hot.md`
- `memory/log.md`
- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\README.md`
- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\docs\safe-agent-contract.md`
- `C:\Users\yrred\Documents\New project 2\twb-marketing-presence-agent\SUBAGENT_HYDRATION_PROMPT.md`

## Checks Run

- Reviewed current TWB-Marketing roadmap, active task brief, safe-agent contract, hot file, and index before editing.
- No executable app code was created or tested.

## Safety Boundary Confirmation

No posting automation, account integration, private scraping, or external notification integration was created. The alerting requirement is scoped to local app state and future user-approved notification behavior.

## Memory-Worthy Notes

- Decision - Alerting and quiet-hours controls are core app requirements.
- Decision - During quiet hours, alert-mute mode should queue low and normal opportunities silently.
- Decision - During quiet hours, sleep-throttle mode should gather only high-importance opportunities until the user is awake.
- Decision - High-importance opportunities should be separated and may interrupt only according to user-configured rules.
- Decision - The app should provide snooze/mute controls and a digest/reminder after quiet hours.
- Warning - Alerting should be tuned to protect attention and surface important review items, not to maximize posting volume.

## Do Not Promote To Memory

- Exact quiet-hours schedule.
- Exact high-importance thresholds.
- Any external notification provider or OS integration choice.

## Follow-Up Recommendations

1. In milestone 1, build the alert center as local UI and mock state.
2. Later, choose whether reminders should be OS notifications, email, mobile push, calendar reminders, or in-app only.
3. Define conservative high-importance rules after testing real opportunity examples.
