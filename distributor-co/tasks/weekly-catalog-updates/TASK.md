---
name: Weekly Catalog Updates
description: Process the weekly batch of product catalog changes — new item setups, attribute updates, price changes, and discontinuations with GS1 validation.
slug: weekly-catalog-updates
assignee: item-data-manager
project: catalog-integrity
schedule:
  timezone: America/Chicago
  startsAt: "2026-04-01T09:00:00-05:00"
  recurrence: weekly-wednesday
---

# Weekly Catalog Updates

1. Process all pending new item setup requests. Validate GS1 compliance for each.
2. Apply queued attribute updates (packaging changes, certification renewals, description updates).
3. Load pending price changes with effective dates. Verify margin impact.
4. Process scheduled discontinuations. Confirm inventory has been cleared at all DCs.
5. Run data quality audit: check completeness rate, flag items missing required fields.
6. Report catalog metrics to Director of Catalog & Pricing: items processed, quality score, backlog.
