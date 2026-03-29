---
name: Daily Sales Monitor
description: Monitor daily sales by category. Flag velocity anomalies, out-of-stock alerts, and shrink indicators. Surface issues before they become problems.
slug: daily-sales-monitor
assignee: category-analyst
project: category-optimization
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-28T08:00:00-05:00"
  recurrence: daily
---

# Daily Sales Monitor

1. Pull daily sales by category from POS data (manual pull until MCP integration available).
2. Flag any category with sales down 10%+ vs prior week average.
3. Identify products with zero scans that should be in stock (out-of-stock candidates).
4. Flag velocity anomalies — sudden spikes or drops that need investigation.
5. Note high-shrink categories that need attention.
6. Summarize findings and share with category managers and VP Merchandising.
