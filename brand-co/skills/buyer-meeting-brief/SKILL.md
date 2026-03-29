---
name: buyer-meeting-brief
description: "Prepare a comprehensive meeting brief for an upcoming retailer buyer meeting. Use before buyer meetings, category reviews, or sell-in presentations."
slug: buyer-meeting-brief
tags:
  - sales
  - meetings
  - retail
  - preparation
---

# Buyer Meeting Brief

Produce a structured one-page meeting brief for an upcoming retailer buyer meeting. Pulls account history, contacts, pipeline, sellsheets, and distribution data into a ready-to-use preparation document.

## When to Use

- User has a buyer meeting coming up and needs to prepare
- User asks to "prep for" or "brief me on" a retailer meeting
- Before category reviews or sell-in presentations
- When onboarding to an unfamiliar account before a first meeting

## Workflow

### Step 1: Identify the Meeting Context

Ask the user (if not already provided):
- Which retailer/account?
- Which buyer contact?
- Date and type of meeting (sell-in, category review, QBR, check-in)
- Any specific products or product families to focus on

### Step 2: Gather Account Intelligence

Run these calls to build the account picture:

1. **Account details**: `mcp__sally-mcp__search_accounts` with the retailer name to get the account record
2. **Account history**: Review the account record for creation date, last activity, account type, and any notes
3. **Contact roster**: `mcp__sally-mcp__search_contacts` filtered to the account — identify the buyer, category manager, and any other contacts
4. **Meeting history**: `mcp__sally-mcp__list_meetings` for past meetings at this account — note frequency, recency, and outcomes
5. **Product families**: `mcp__sally-mcp__list_account_families` to see which product families are already associated with the account

### Step 3: Gather Pipeline Intelligence

1. **Active opportunities**: `mcp__sally-mcp__search_opportunities` filtered to the account — list all open opportunities with stage, value, and last activity
2. **Pipeline metrics**: `mcp__sally-mcp__get_pipeline_metrics` for overall pipeline context (helps frame this account's relative importance)
3. **Upcoming activities**: `mcp__sally-mcp__get_upcoming` to check for any scheduled follow-ups or deadlines

### Step 4: Gather Product and Collateral

1. **Product details**: `mcp__sally-mcp__search_products` for the products relevant to this meeting — get current pricing, pack size, UPC, and key attributes
2. **Sellsheets**: `mcp__sally-mcp__get_sellsheet` for each relevant product — confirm sellsheets are current and available for the meeting
3. If sellsheets are missing or outdated, flag this in the brief

### Step 5: Gather Distribution Context

1. **Distributor codes**: `mcp__sally-mcp__get_distributor_codes` to verify distributor authorization status for the products being discussed
2. **Distribution families**: `mcp__sally-mcp__get_distributor_families` for family-level distribution coverage
3. Note any gaps: products the buyer might want that are not yet authorized at the relevant DC

### Step 6: Compile the Brief

Format the brief using the structure in `references/buyer-meeting-checklist.md`. The brief should follow this outline:

```
# Meeting Brief: [Retailer Name]
**Date**: [meeting date]  |  **Type**: [sell-in / category review / QBR / check-in]
**Buyer**: [name, title]  |  **Location**: [if applicable]

## Account Snapshot
- Account since: [date]
- Last meeting: [date] — [outcome summary]
- Current product families: [list]
- Total active opportunities: [count] valued at [total]

## Key Contacts
| Name | Title | Last Contact | Notes |
|------|-------|-------------|-------|
| ...  | ...   | ...         | ...   |

## Pipeline Status
| Opportunity | Stage | Value | Days in Stage | Next Step |
|-------------|-------|-------|---------------|-----------|
| ...         | ...   | ...   | ...           | ...       |

## Products for Discussion
| Product | Pack Size | Current Price | Sellsheet | DC Authorization |
|---------|-----------|---------------|-----------|-----------------|
| ...     | ...       | ...           | Yes / No  | Yes / No        |

## Distribution Status
- Authorized DCs: [list]
- Gaps: [products not yet authorized at relevant DCs]

## Talking Points
1. [Generated from pipeline context — e.g., "Follow up on Q1 promotional performance"]
2. [Generated from opportunity stage — e.g., "Push for authorization on new SKU"]
3. [Generated from meeting history — e.g., "Buyer mentioned interest in X last meeting"]

## Preparation Checklist
- [ ] Sellsheets printed/loaded for all products
- [ ] Samples packed (if applicable)
- [ ] Pricing confirmed with latest distributor costs
- [ ] Competitive positioning notes reviewed
- [ ] Previous meeting notes reviewed
```

### Step 7: Flag Gaps and Risks

At the end of the brief, call out:
- **Missing data**: Anything the CRM doesn't have that the user should research (SPINS data, competitive shelf sets, promotional calendars)
- **Stale records**: Contacts not updated recently, opportunities stuck in a stage
- **Distribution risks**: Products being pitched that lack DC authorization

## Notes

- The `buyer-meeting-prep` MCP prompt provides a useful starting framework — invoke it if available, then supplement with the tool calls above
- If the user provides a specific meeting record ID, start from that meeting and work outward to gather context
- Keep the brief to one page equivalent — prioritize actionable intelligence over exhaustive data dumps
- Always include the preparation checklist — it serves as the user's pre-meeting to-do list
