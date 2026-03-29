---
name: Daily Pipeline Check
description: Review the multi-brand pipeline for stalls, coverage gaps, and upcoming deadlines across all territories.
slug: daily-pipeline-check
assignee: territory-manager
project: multi-brand-sales
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-28T09:00:00-05:00"
  recurrence: daily
---

# Daily Pipeline Check

1. Pull all active opportunities across assigned territory using search_opportunities.
2. Flag any opportunity stalled in the same stage for 14+ days.
3. Check pipeline velocity against benchmarks using get_pipeline_metrics.
4. Verify all scheduled buyer meetings for the next 48 hours have prep completed.
5. Identify brand-retailer coverage gaps — retailers carrying fewer brands than expected.
6. Report stalls and gaps to VP Sales with recommended actions.
