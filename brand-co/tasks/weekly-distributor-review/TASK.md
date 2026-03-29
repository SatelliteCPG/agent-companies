---
name: Weekly Distributor Review
description: Monday morning distribution gap analysis. Cross-reference distributor DC authorization against active pipeline opportunities. Identify authorization gaps, setup blockers, and white-space sell-in opportunities.
slug: weekly-distributor-review
assignee: distributor-liaison
project: distribution-coverage
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-28T10:00:00-05:00"
  recurrence: weekly
---

# Weekly Distributor Review

1. Pull all active opportunities via `search_opportunities`
2. For each opportunity's target retailer, check DC coverage via `get_distributor_families` and `search_distribution_centers`
3. Verify item codes are active for sell-in targets via `get_distributor_codes`
4. Use `list_account_families` to cross-reference product families across accounts and distributors
5. Use `list_distributors` to check for new distributor network additions
6. Run the `distributor-check` prompt for structured authorization verification
7. Categorize gaps: authorized-but-no-pipeline, pipeline-but-no-authorization, incomplete-setup
8. Report to Sales Director with prioritized gap list and recommended actions
