---
name: partner-pipeline-dashboard
description: "Generate a cross-brand pipeline view grouped by brand with rollup metrics. Use during weekly pipeline reviews or when preparing portfolio-level status updates."
slug: partner-pipeline-dashboard
tags:
  - sales
  - pipeline
  - analytics
  - multi-brand
---

# Partner Pipeline Dashboard

Generate a cross-brand pipeline view that shows pipeline health grouped by brand, retailer, or territory with rollup metrics. Designed for brokers managing 50-100 brands who need a portfolio-level view of all active opportunities.

## When to Use

- Weekly pipeline review (typically Monday morning)
- Preparing a portfolio status update for Managing Partner
- User asks for "pipeline across all brands" or "show me the dashboard"
- Before brand principal meetings to contextualize one brand's performance vs portfolio

## Workflow

### Step 1: Pull Aggregate Pipeline Metrics

Call `mcp__sally-mcp__get_pipeline_metrics` to get the high-level pipeline snapshot:
- Total pipeline value across all brands
- Opportunity count by stage
- Average deal size
- Pipeline velocity indicators

### Step 2: Pull All Active Opportunities

Call `mcp__sally-mcp__search_opportunities` to retrieve all open/active opportunities. For each, note:
- Brand/company association
- Retailer/account
- Current stage
- Days in current stage
- Last activity date
- Expected close date
- Estimated value

### Step 3: Group by Brand

Aggregate opportunities by brand to build the brand-level view:

```
# Partner Pipeline Dashboard — Week of [date]

## Portfolio Summary
- Total pipeline value: $[X] across [N] brands
- Active opportunities: [N]
- Opportunities by stage: [breakdown]
- Deals expected to close this month: [N] worth $[X]

## Pipeline by Brand (sorted by pipeline value)

| Brand | Active Opps | Pipeline Value | Avg Stage | Stalled | Next Close |
|-------|------------|---------------|-----------|---------|------------|
| [Brand 1] | [N] | $[X] | [avg] | [N] | [date] |
| [Brand 2] | [N] | $[X] | [avg] | [N] | [date] |
| ...   | ...        | ...           | ...       | ...     | ...        |
| **Total** | **[N]** | **$[X]** | | **[N]** | |
```

### Step 4: Group by Retailer

Aggregate by retailer to show where the broker has the deepest relationships:

```
## Pipeline by Retailer (sorted by opportunity count)

| Retailer | Brands Active | Total Opps | Pipeline Value | Last Meeting |
|----------|-------------|-----------|---------------|-------------|
| [Retailer 1] | [N] | [N] | $[X] | [date] |
| [Retailer 2] | [N] | [N] | $[X] | [date] |
| ...      | ...         | ...       | ...           | ...         |
```

### Step 5: Identify Stalls and Gaps

Apply stall thresholds from `references/partner-pipeline-thresholds.md`:

```
## Attention Required

### Stalled Opportunities (14+ days in stage)
| Brand | Retailer | Opportunity | Stage | Days Stalled | Value |
|-------|----------|-------------|-------|-------------|-------|
| ...   | ...      | ...         | ...   | ...         | ...   |

### Brands with No Active Pipeline
| Brand | Last Opportunity | Last Meeting | Recommended Action |
|-------|-----------------|-------------|-------------------|
| ...   | ...             | ...         | ...               |

### Retailers with Low Brand Coverage
| Retailer | Brands Carried | Portfolio Brands Relevant | Gap |
|----------|---------------|--------------------------|-----|
| ...      | [N]           | [N]                      | [N] |
```

### Step 6: Generate Portfolio Action Items

For each flagged item, generate specific actions:
- **Stalled deal**: "Contact [buyer] at [retailer] about [brand] — last activity [date]."
- **Brand gap**: "[Brand] has no active pipeline. Last opportunity was [date]. Consider targeting [retailer] based on category fit."
- **Retailer coverage gap**: "[Retailer] carries [N] of [N] relevant brands. Cross-sell opportunity for [brand list]."

## Notes

- The `pipeline-review` MCP prompt provides a useful starting framework — invoke it for the top-level view, then layer brand-level grouping
- Brands with zero pipeline should be flagged but not alarmed — some brands may be seasonal or in onboarding
- Cross-brand coverage gaps at retailers are the highest-value insight — these are the upsell opportunities
- Use `search_accounts` and `list_account_families` to identify which brands each retailer already carries
