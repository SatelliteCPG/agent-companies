---
name: Weekly Buyer Meeting Prep
description: Prepare multi-brand meeting briefs for all buyer meetings scheduled in the coming week. Aggregate sell sheets, pipeline, and distribution status per retailer.
slug: weekly-buyer-meeting-prep
assignee: broker-sales-rep
project: multi-brand-sales
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-30T08:00:00-05:00"
  recurrence: weekly-monday
---

# Weekly Buyer Meeting Prep

1. Pull all buyer meetings scheduled for the week using list_meetings and get_upcoming.
2. For each meeting, identify which brands from the portfolio are relevant to the buyer's category set.
3. Run multi-brand-meeting-brief skill for each meeting — aggregate sell sheets, pricing, promo calendars, and distribution status.
4. Verify sellsheets are current for all products being pitched using search_sellsheets.
5. Confirm distributor DC authorization for all products using get_distributor_codes.
6. Flag any gaps — missing sellsheets, inactive distributor codes, stale product pricing.
7. Deliver completed briefs to the meeting files by end of day Monday.
