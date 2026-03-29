---
name: brand-performance-report
description: "Generate a monthly performance summary for a brand principal with pipeline activity, placements, voids, deductions, and priorities. Use at month-end or when brand principals request status updates."
slug: brand-performance-report
tags:
  - reporting
  - client-services
  - monthly
  - multi-brand
---

# Brand Performance Report

Generate a monthly performance report for a single brand principal. This is the broker's accountability document — it shows the brand founder or VP Sales exactly what the broker accomplished on their behalf during the month.

## When to Use

- 1st of each month — generate for every brand in the portfolio
- Brand principal requests a status update
- User asks to "pull the report for [brand]" or "how is [brand] doing"
- Before brand sync calls to prepare talking points

## Workflow

### Step 1: Identify the Brand

Ask the user (if not already provided):
- Which brand?
- Which reporting period? (default: previous calendar month)

Look up the brand with `mcp__sally-mcp__get_company` or `mcp__sally-mcp__search_accounts` to confirm the brand record.

### Step 2: Pull Pipeline Activity

1. Call `mcp__sally-mcp__search_opportunities` filtered to this brand for the reporting period
2. Categorize opportunities:
   - **Created**: New opportunities opened during the month
   - **Advanced**: Opportunities that moved forward in stage
   - **Won**: Opportunities closed-won (new authorizations)
   - **Lost**: Opportunities closed-lost
   - **Active**: Still open at month-end
3. Call `mcp__sally-mcp__get_pipeline_metrics` for velocity context

### Step 3: Pull Meeting Activity

1. Call `mcp__sally-mcp__list_meetings` filtered to this brand for the reporting period
2. Count meetings by type: buyer meetings, broker syncs, category reviews
3. Note key outcomes from meeting records

### Step 4: Pull Distribution Data

1. Call `mcp__sally-mcp__get_distributor_codes` for the brand's products
2. Call `mcp__sally-mcp__get_distributor_families` for family-level coverage
3. Note any new DC authorizations gained or codes activated during the month
4. Note any distribution gaps or pending setups

### Step 5: Compile Void and Deduction Data

1. **Void data**: Summarize voids identified and closed for this brand during the month. Use `mcp__sally-mcp__search_opportunities` filtered for void-related opportunities.
2. **Deduction data**: Summarize deductions disputed and recovered for this brand. Use `mcp__sally-mcp__search_accounts` for account-level deduction context.

### Step 6: Generate the Report

```
# Monthly Performance Report: [Brand Name]
**Period**: [Month Year]  |  **Prepared by**: [Broker Name]

## Executive Summary
[2-3 sentences on the month's highlights and lowlights]

## Pipeline Activity
| Metric | This Month | Prior Month | Trend |
|--------|-----------|-------------|-------|
| New opportunities | [N] | [N] | [up/down/flat] |
| Opportunities advanced | [N] | [N] | [up/down/flat] |
| Won (new authorizations) | [N] | [N] | [up/down/flat] |
| Lost | [N] | [N] | [up/down/flat] |
| Active pipeline value | $[X] | $[X] | [up/down/flat] |

## New Placements
| Retailer | Product | Authorization Date | Expected First Ship |
|----------|---------|-------------------|-------------------|
| ...      | ...     | ...               | ...               |

## Meeting Activity
- Total buyer meetings: [N]
- Key outcomes:
  - [Meeting 1 outcome]
  - [Meeting 2 outcome]

## Distribution Status
| Distributor | Active Codes | Pending | New This Month |
|-------------|-------------|---------|----------------|
| ...         | ...         | ...     | ...            |

## Void Closure
- Voids identified: [N]
- Voids closed: [N]
- Open voids: [N]

## Deduction Recovery
- Deductions received: $[X]
- Disputes filed: $[X]
- Recovered: $[X]
- Recovery rate: [X]%

## Next Month Priorities
1. [Priority 1 — specific action with retailer/product target]
2. [Priority 2]
3. [Priority 3]
```

### Step 7: Context and Comparison

If this is not the first month, compare against prior months:
- Is pipeline growing or shrinking?
- Are wins accelerating or decelerating?
- Is void closure rate improving?
- Are deduction recovery amounts trending up?

Flag any concerning trends and recommend actions.

## Notes

- The `account-deep-dive` MCP prompt provides useful per-account context when drilling into specific retailer relationships
- Keep the report to one-page equivalent — brand principals want a dashboard, not a novel
- Always end with specific next-month priorities — this sets expectations with the brand principal
- If data is incomplete (new brand, limited history), note the limitation and set a baseline
