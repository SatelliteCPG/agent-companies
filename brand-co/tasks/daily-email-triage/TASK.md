---
name: Daily Email Triage
description: Process all inbound email threads from the previous day. Extract entities, update CRM contacts, create meetings and opportunities, and process sample requests. Zero unprocessed emails by 9am.
slug: daily-email-triage
assignee: sales-coordinator
project: retail-sell-in
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-28T08:00:00-05:00"
  recurrence: daily
---

# Daily Email Triage

1. Process each inbound email thread via `process_email_thread`
2. Search for existing contacts via `search_contacts`
3. Create new contacts via `create_contact` or update via `update_contact`
4. Create meetings from meeting requests via `create_meeting`
5. Create or update opportunities via `create_opportunity` / `update_opportunity`
6. Process sample requests via `create_sample_request`
7. Use `email-to-crm-upsert` prompt for structured extraction
8. Use `email-thread-summary` prompt for quick thread summaries
9. Flag anything requiring Sales Director attention
