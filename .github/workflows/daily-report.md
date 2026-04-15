---
on:
  schedule:
    - cron: "0 9 * * *"
permissions:
  contents: read
  actions: read
  pull-requests: read
  issues: read
network: defaults
safe-outputs:
  create-issue:
    labels:
      - daily-report
---

# daily-report

Create one daily issue report covering repository activity from the past 24 hours.

Requirements:
- Run from the schedule trigger (9 AM).
- Gather and summarize:
  - Commits pushed in the last 24 hours
  - Pull requests opened, updated, merged, or closed in the last 24 hours
  - Issues opened or closed in the last 24 hours
  - CI/CD failures from workflow runs in the last 24 hours
- Create exactly one issue using `safe-outputs` `create-issue` (do not use direct write tools).
- If no activity is found for a category, explicitly state that category had no activity.
- Use clear markdown sections and include UTC timestamp boundaries for the 24-hour window.
