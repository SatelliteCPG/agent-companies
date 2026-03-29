---
name: Daily Pipeline Check
description: Quick morning pipeline scan after email triage. Update opportunity stages from morning emails, verify meeting briefs are prepared for today, and flag stalled opportunities to the Sales Director.
slug: daily-pipeline-check
assignee: sales-coordinator
project: retail-sell-in
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-28T09:00:00-05:00"
  recurrence: daily
---

# Daily Pipeline Check

1. Run `search_opportunities` to check for stage updates needed from morning email triage
2. Check `get_upcoming` for today's scheduled meetings
3. Verify buyer meeting briefs are prepared for each meeting (run `buyer-meeting-prep` if not)
4. Identify stalled opportunities — no activity in 14+ days
5. Flag stalled deals and missing briefs to the Sales Director
6. Update any opportunity stages that changed due to morning email processing via `update_opportunity`
