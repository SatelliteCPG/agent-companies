---
name: multi-brand-meeting-brief
description: "Aggregate sell sheets and pipeline across N brands for one retailer meeting. Use before buyer meetings where the broker represents multiple brands to a single buyer."
slug: multi-brand-meeting-brief
tags:
  - sales
  - meetings
  - multi-brand
  - preparation
---

# Multi-Brand Meeting Brief

Produce a structured meeting brief for an upcoming retailer buyer meeting where the broker represents multiple brands. Unlike a single-brand brief, this aggregates sell sheets, pipeline, pricing, promotions, and distribution status across 3-10 brands for a single buyer session.

## When to Use

- Broker has a buyer meeting coming up and needs a multi-brand prep
- User asks to "prep for" or "brief me on" a retailer meeting
- Before category reviews where multiple portfolio brands are relevant
- When a broker rep needs a unified pitch document covering the full portfolio

## Workflow

### Step 1: Identify the Meeting Context

Ask the user (if not already provided):
- Which retailer/account?
- Which buyer contact?
- Date and type of meeting (sell-in, category review, QBR, check-in)
- Which brands from the portfolio are relevant? (or "all relevant brands")

### Step 2: Identify Relevant Brands

1. **Account lookup**: Call `mcp__sally-mcp__search_accounts` with the retailer name to get the account record
2. **Current brand families**: Call `mcp__sally-mcp__list_account_families` to see which brands/product families the retailer already carries
3. **Portfolio match**: Cross-reference the broker's full brand portfolio against the buyer's category set to identify all relevant brands — both existing and prospective

### Step 3: Gather Per-Brand Intelligence

For each relevant brand, collect:

1. **Active opportunities**: `mcp__sally-mcp__search_opportunities` filtered to this retailer AND this brand — list stage, value, and last activity
2. **Product details**: `mcp__sally-mcp__search_products` and `mcp__sally-mcp__get_product` for each brand's products relevant to this buyer
3. **Sellsheets**: `mcp__sally-mcp__get_sellsheet` and `mcp__sally-mcp__search_sellsheets` for each brand — confirm current and available
4. **Distribution status**: `mcp__sally-mcp__get_distributor_codes` to verify DC authorization for each brand's products
5. **Distribution families**: `mcp__sally-mcp__get_distributor_families` for family-level coverage

### Step 4: Gather Account-Level Context

1. **Contact roster**: `mcp__sally-mcp__search_contacts` filtered to the retailer — identify the buyer, category manager, and supporting contacts
2. **Meeting history**: `mcp__sally-mcp__list_meetings` for past meetings at this retailer — note frequency, recency, and outcomes across all brands
3. **Upcoming activities**: `mcp__sally-mcp__get_upcoming` for any scheduled follow-ups
4. **Pipeline metrics**: `mcp__sally-mcp__get_pipeline_metrics` for overall context

### Step 5: Compile the Multi-Brand Brief

Format using the structure in `references/multi-brand-meeting-template.md`:

```
# Multi-Brand Meeting Brief: [Retailer Name]
**Date**: [date]  |  **Type**: [sell-in / category review / QBR]
**Buyer**: [name, title]  |  **Brands Covered**: [count]

## Account Snapshot
- Account since: [date]
- Brands currently carried: [list]
- Total active opportunities: [N] across [N] brands
- Last meeting: [date] — [outcome]

## Brand-by-Brand Summary

### [Brand 1 Name]
**Status**: [Existing / Prospective]
| Product | Pack Size | Price | Sellsheet | DC Auth | Opportunity Stage |
|---------|-----------|-------|-----------|---------|-------------------|
| ...     | ...       | ...   | Yes/No    | Yes/No  | ...               |
**Talking Point**: [Generated from pipeline context]

### [Brand 2 Name]
**Status**: [Existing / Prospective]
| Product | Pack Size | Price | Sellsheet | DC Auth | Opportunity Stage |
|---------|-----------|-------|-----------|---------|-------------------|
| ...     | ...       | ...   | Yes/No    | Yes/No  | ...               |
**Talking Point**: [Generated from pipeline context]

[Repeat for each brand]

## Cross-Brand Opportunities
- [Portfolio synergy — e.g., "Brands X and Y fill different price tiers in natural snacks"]
- [Category gap — e.g., "Buyer carries no organic frozen; Brand Z fills this gap"]
- [Promotional bundle — e.g., "Brands A and B can run complementary endcap"]

## Distribution Status Summary
| Brand | Products Authorized | Products Pending | DC Gaps |
|-------|-------------------|-----------------|---------|
| ...   | ...               | ...             | ...     |

## Preparation Checklist
- [ ] Sellsheets printed/loaded for all brands
- [ ] Samples packed per brand (if applicable)
- [ ] Pricing confirmed with latest distributor costs per brand
- [ ] Previous meeting notes reviewed
- [ ] Cross-brand positioning story prepared
```

### Step 6: Flag Gaps and Risks

Call out:
- **Missing sellsheets**: Brands without current sellsheets
- **Distribution gaps**: Products being pitched that lack DC authorization
- **Stale data**: Opportunities or contacts not updated recently
- **Brand conflicts**: Any portfolio brands that compete with each other at this retailer

## Notes

- The `buyer-meeting-prep` MCP prompt provides a useful single-brand starting framework — invoke it once per brand, then aggregate
- Keep the brief actionable — the broker rep walks into the meeting with this as their playbook
- Cross-brand opportunities are the highest-value section — this is what a broker can offer that a single brand cannot
- Always include the preparation checklist as the pre-meeting to-do list
