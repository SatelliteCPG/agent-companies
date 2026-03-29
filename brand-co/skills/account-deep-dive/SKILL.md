---
name: account-deep-dive
description: "Conduct a comprehensive analysis of a retail account — contacts, opportunities, meetings, products, and distribution. Use before account reviews, QBRs, or when onboarding to a new account."
slug: account-deep-dive
tags:
  - sales
  - accounts
  - analysis
---

# Account Deep Dive

Conduct a comprehensive analysis of a single retail account, compiling everything the CRM knows into a structured account profile. This is the most thorough account analysis skill — use it for strategic reviews, not routine check-ins.

## When to Use

- Preparing for a quarterly business review (QBR)
- Onboarding to a new account and need full context
- Account strategy session or annual planning
- User asks for a "deep dive," "full picture," or "everything we know" about an account
- Handing off an account to a new team member

## Workflow

### Step 1: Identify the Account

1. Call `mcp__sally-mcp__search_accounts` with the account name or identifier
2. Confirm the correct account with the user if multiple matches
3. Note the account ID for subsequent queries

### Step 2: Account Profile

From the account record, extract:
- Account name, type, and status
- Creation date (how long has this been a relationship?)
- Any account-level notes or tags
- Parent company or group (if applicable)

### Step 3: Relationship Map — Contacts

1. Call `mcp__sally-mcp__search_contacts` filtered to this account
2. For each contact, capture: name, title, role, email, phone, last contact date
3. Categorize contacts by role:
   - **Decision makers**: Buyers, category managers, VPs
   - **Influencers**: Assistant buyers, merchandising coordinators
   - **Operations**: Receiving, store managers (if tracked)
   - **Brokers**: Any broker contacts associated with this account
4. Identify gaps: Is there a primary buyer contact? Is the category manager known?

### Step 4: Opportunity Pipeline

1. Call `mcp__sally-mcp__search_opportunities` filtered to this account
2. Separate into:
   - **Open opportunities**: Current pipeline items with stage, value, age
   - **Won opportunities**: Historical wins — what products got authorized and when
   - **Lost opportunities**: Historical losses — what was rejected and why (if reason captured)
3. Calculate: total pipeline value, win rate at this account, average deal cycle time

### Step 5: Meeting History

1. Call `mcp__sally-mcp__list_meetings` filtered to this account
2. Build a timeline of all meetings: date, attendees, type, outcomes
3. Calculate meeting frequency: how often is the team engaging this account?
4. Note the most recent meeting and its outcomes — this is critical context

### Step 6: Product Coverage

1. Call `mcp__sally-mcp__list_account_families` to see which product families are associated with this account
2. Call `mcp__sally-mcp__search_products` to get the full product catalog
3. Build a product coverage matrix:
   - Products currently authorized at this account
   - Products pitched but not yet authorized
   - Products not yet pitched (whitespace)
4. For authorized products, note any sellsheet availability via `mcp__sally-mcp__get_sellsheet`

### Step 7: Distribution Status

1. Call `mcp__sally-mcp__search_distribution_centers` to identify DCs that serve this account's geography
2. Call `mcp__sally-mcp__get_distributor_families` to check authorization at relevant DCs
3. Map the connection: Is every authorized product available at the DCs that serve this retailer?
4. Flag any distribution gaps that could block shelf availability

### Step 8: Compile the Account Profile

Format using the structure in `references/account-review-template.md`:

```
# Account Deep Dive: [Retailer Name]
**Generated**: [date]  |  **Account Since**: [date]  |  **Status**: [active/dormant/new]

## Executive Summary
[2-3 sentence overview: relationship health, pipeline status, key opportunity or risk]

## Relationship Map
### Decision Makers
| Name | Title | Email | Last Contact | Engagement Level |
|------|-------|-------|-------------|-----------------|
| ...  | ...   | ...   | ...         | Active/Dormant  |

### Other Contacts
| Name | Title | Role | Last Contact |
|------|-------|------|-------------|
| ...  | ...   | ...  | ...         |

### Contact Gaps
- [ ] [Missing roles — e.g., "No category manager identified"]

## Opportunity Pipeline
### Active Opportunities
| Opportunity | Product Family | Stage | Value | Days in Stage | Next Step |
|-------------|---------------|-------|-------|---------------|-----------|
| ...         | ...           | ...   | ...   | ...           | ...       |

### Historical Performance
- Total opportunities: [N]
- Won: [N] ($[X]) | Lost: [N] ($[X]) | Open: [N] ($[X])
- Win rate: [X]%
- Average cycle time: [X] days

## Product Coverage
| Product Family | Status | Sellsheet | Notes |
|---------------|--------|-----------|-------|
| [Family 1]    | Authorized | ✓ Current | Carrying since [date] |
| [Family 2]    | Pitched | ✓ Current | In qualification stage |
| [Family 3]    | Not pitched | ✗ Needs update | Whitespace opportunity |

## Distribution Status
| DC | Distributor | [Family 1] | [Family 2] | [Family 3] |
|----|------------|------------|------------|------------|
| [DC serving this account] | UNFI | ✓ | ✗ | — |

### Distribution Gaps
- [List any product-DC gaps that affect this account]

## Meeting History (Last 6 Months)
| Date | Type | Attendees | Key Outcomes |
|------|------|-----------|-------------|
| ...  | ...  | ...       | ...         |

**Meeting frequency**: [X] meetings per month (avg over last 6 months)
**Last meeting**: [date] — [outcome]

## Competitive Position
**Note**: Competitive data requires SPINS integration (not yet available).
- Known competitors at this retailer: [if captured in CRM notes]
- Shelf position: [if known]

## Action Plan
1. [Highest-priority action — e.g., "Schedule follow-up with buyer on stalled proposal"]
2. [Distribution action — e.g., "Initiate authorization at [DC] for [product family]"]
3. [Relationship action — e.g., "Identify and connect with category manager"]
4. [Product action — e.g., "Update sellsheet for [product] before next meeting"]
5. [Strategic action — e.g., "Prepare for Q3 category review — submission due [date]"]
```

## Notes

- The `account-deep-dive` MCP prompt provides a starting framework — invoke it if available, then supplement with the detailed tool calls above
- This skill produces the most comprehensive output of all brand-co skills. For lighter-weight account lookups, use `buyer-meeting-brief` instead.
- The action plan section is the most valuable output — prioritize generating specific, actionable next steps over exhaustive data presentation
- If the account is new (< 30 days), skip historical analysis sections and focus on the onboarding checklist
