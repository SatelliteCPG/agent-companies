---
name: Daily Order Monitor
description: Monitor order fulfillment, flag low-inventory DCs, track fill rate exceptions.
slug: daily-order-monitor
assignee: demand-planner
project: distribution-expansion
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-28T07:00:00-05:00"
  recurrence: daily
---

# Daily Order Monitor

1. Pull overnight order fulfillment data.
2. Flag any DCs with inventory below safety stock thresholds.
3. Track fill rate exceptions — any DC below 95% fill rate.
4. Escalate critical out-of-stock situations to distribution-manager.
5. Update demand forecast with latest order velocity data.
