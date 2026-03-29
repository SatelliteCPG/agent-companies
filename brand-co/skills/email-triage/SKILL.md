---
name: email-triage
description: "Triage inbound emails, extract CRM-relevant information, create or update contacts and accounts, and log activities. Use when processing sales emails or buyer communications."
slug: email-triage
tags:
  - sales
  - email
  - crm
  - daily
---

# Email Triage and CRM Capture

Process inbound email threads to extract entities, update the CRM, and log all activities. This is the most frequent brand workflow — run multiple times daily, typically first thing each morning.

## When to Use

- User pastes an email thread and asks to process it
- User asks to "triage" or "process" emails
- User forwards buyer, broker, or distributor communications
- User asks to update CRM from an email

## Workflow

### Step 1: Extract Email Metadata

Use `mcp__sally-mcp__process_email_thread` to parse the email thread. This extracts:
- Sender and recipient names, titles, companies
- Dates, times, locations mentioned
- Action items and commitments
- Meeting references or scheduling intent
- Product or SKU mentions
- Sample request references

### Step 2: Match Existing Contacts

For each person identified in the email:

1. Call `mcp__sally-mcp__search_contacts` with the person's name and/or email
2. If a match is found, check whether any fields need updating (title change, new email, new phone)
3. If fields changed, call `mcp__sally-mcp__update_contact` with the updated fields
4. If no match is found, proceed to Step 3

### Step 3: Create New Contacts

For unmatched contacts:

1. Determine the contact's role from email context:
   - BUYER — works at a retailer, makes purchasing decisions
   - BROKER — works at a broker/partner firm, represents the brand
   - DISTRIBUTOR — works at UNFI, KeHE, or other distributor
   - OTHER — vendor, consultant, internal team member
2. Call `mcp__sally-mcp__create_contact` with all available fields
3. Note: always associate the contact with their company — search for the company first

### Step 4: Match or Create Accounts

For each company referenced in the email:

1. Call `mcp__sally-mcp__search_accounts` with the company name
2. If no match, call `mcp__sally-mcp__create_account` with available details
3. Link new contacts to the appropriate account

### Step 5: Detect and Create Meetings

If the email contains meeting-related content (scheduling, confirmation, recap):

1. Extract: date, time, location, attendees, agenda/purpose
2. Call `mcp__sally-mcp__create_meeting` with the extracted details
3. Link the meeting to the relevant account and contacts

### Step 6: Detect and Process Opportunities

If the email discusses:
- A new product listing or authorization
- A category review submission
- A promotional placement
- A pricing negotiation

Then:
1. Call `mcp__sally-mcp__search_opportunities` to check for existing opportunities at that account
2. If found, call `mcp__sally-mcp__update_opportunity` with any new information (stage change, notes)
3. If new, call `mcp__sally-mcp__create_opportunity` with details from the email

### Step 7: Detect Sample Requests

If the email references product samples (request, shipment, follow-up):

1. Call `mcp__sally-mcp__create_sample_request` with product, recipient, and shipping details
2. Note the sample purpose (buyer evaluation, store demo, trade show)

### Step 8: Summarize Actions Taken

Present a structured summary to the user:

```
## Email Triage Summary

**Thread**: [subject line]
**From**: [sender] → **To**: [recipients]

### CRM Actions
- Updated contact: [name] — new title: [title]
- Created contact: [name] at [company] (BUYER)
- Created meeting: [date] with [attendees] at [location]
- Updated opportunity: [name] — moved to [stage]

### Follow-up Items
- [ ] Send samples to [contact] by [date]
- [ ] Confirm meeting details with [contact]
- [ ] Prepare sellsheet for [product]
```

## Decision Rules

See `references/email-triage-patterns.md` for classification patterns by email type.

### Email Classification Priority

1. **Meeting-related** — Always create/update meeting records first
2. **Opportunity-related** — Update pipeline before logging other activities
3. **New contact** — Create contact before associating with meetings or opportunities
4. **Informational** — Log as activity note on the relevant account

### Deduplication

- Always search before creating. Use email address as the primary dedup key for contacts.
- For meetings, check for existing meetings within +/- 1 day at the same account before creating duplicates.
- For opportunities, match on account + product family + approximate timeframe.

## Error Handling

- If `process_email_thread` returns incomplete data, ask the user to clarify missing fields
- If contact search returns multiple matches, present options to the user for disambiguation
- If account cannot be determined from context, ask the user before creating a new account
