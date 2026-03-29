---
name: Weekly Void Status Check
description: Run a full void analysis comparing authorized items against distributor DC stocking. Surface gaps, prioritize closures, and track progress.
slug: weekly-void-status-check
assignee: void-specialist
project: multi-brand-sales
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-30T10:00:00-05:00"
  recurrence: weekly-monday
---

# Weekly Void Status Check

1. Pull all authorized product-DC combinations using get_distributor_codes and get_distributor_families.
2. Cross-reference against actual stocking/movement data from search_distribution_centers.
3. Identify voids — authorized items not flowing through DCs.
4. Run void-closure-report skill to generate structured gap analysis by brand and retailer.
5. Prioritize voids by revenue impact — high-velocity brands at high-volume retailers first.
6. Update void closure tracking with status changes from prior week.
7. Report void metrics to VP Sales: total voids, closures this week, aging voids, and revenue impact.
