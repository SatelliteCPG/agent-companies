---
name: supplier-scorecard-generator
description: "Generate a supplier performance scorecard with fill rate, OTIF, shelf-life, quality, and responsiveness KPIs. Use when reviewing supplier performance, preparing for supplier meetings, or conducting tier reviews."
slug: supplier-scorecard-generator
tags:
  - suppliers
  - scorecard
  - performance
  - monthly
---

# Supplier Scorecard Generator

Generate a structured supplier performance scorecard covering fill rate, OTIF, shelf-life compliance, quality, and responsiveness. Designed for monthly scoring of 10K+ suppliers at national distributor scale.

## When to Use

- Monthly supplier scorecard generation cycle (1st of each month)
- User asks to review a specific supplier's performance
- Preparing for a supplier performance review meeting
- User asks about supplier tier status or history
- Evaluating whether to expand or reduce a supplier's DC coverage

## Workflow

### Step 1: Identify the Supplier

Ask the user (if not already provided):
- Supplier name or account ID
- Scoring period (default: prior calendar month)
- Is this a single supplier scorecard or a batch review?

### Step 2: Gather Supplier Profile

1. Call `mcp__sally-mcp__search_accounts` with the supplier name to get the account record
2. Call `mcp__sally-mcp__get_company` for company-level details
3. Call `mcp__sally-mcp__search_contacts` to identify key supplier contacts
4. Call `mcp__sally-mcp__search_opportunities` to check for any active opportunities or onboarding records

### Step 3: Gather Distribution Footprint

1. Call `mcp__sally-mcp__get_distributor_codes` to see which DCs carry this supplier's products
2. Call `mcp__sally-mcp__get_distributor_families` to understand product family coverage
3. Call `mcp__sally-mcp__search_products` filtered by brand/supplier to get the product catalog
4. Note total SKU count and DC coverage breadth

### Step 4: Compile Performance Data

**Note**: Most performance data comes from ERP/WMS systems, not MCP tools. The scorecard template below should be populated with data from those operational systems. MCP tools provide the supplier profile and distribution context.

#### Fill Rate (30%)
- Source: PO vs. ASN reconciliation from ERP
- Calculate: (Units shipped / Units ordered) x 100
- Benchmark: > 97% = excellent, 95-97% = acceptable, < 95% = needs improvement
- No MCP tool for fill rate data yet

#### On-Time In-Full — OTIF (25%)
- Source: Receiving records from WMS
- Calculate: (Orders received complete and on time / Total orders) x 100
- Benchmark: > 95% = excellent, 90-95% = acceptable, < 90% = needs improvement
- No MCP tool for OTIF data yet

#### Shelf-Life Compliance (20%)
- Source: Receiving inspection from WMS
- Calculate: (Receipts with > 75% shelf life remaining / Total receipts) x 100
- Benchmark: > 99% = excellent, 97-99% = acceptable, < 97% = needs improvement
- No MCP tool for shelf-life data yet

#### Quality (15%)
- Source: Quality management system
- Calculate: (Units with quality issues / Total units received) x 100 — invert for score
- Include: damaged cases, labeling errors, product defects, recalls
- Benchmark: < 0.5% issue rate = excellent, 0.5-1% = acceptable, > 1% = needs improvement
- No MCP tool for quality data yet

#### Responsiveness (10%)
- Source: Communication logs, CRM activity
- Measure: Average response time to distributor inquiries and claims
- You can use `mcp__sally-mcp__search_accounts` to review account activity notes
- Benchmark: < 24 hours = excellent, 24-48 hours = acceptable, > 48 hours = needs improvement

### Step 5: Calculate Composite Score and Tier

Apply weighted formula:
```
Composite = (Fill Rate Score x 0.30) + (OTIF Score x 0.25) + (Shelf Life Score x 0.20) + (Quality Score x 0.15) + (Responsiveness Score x 0.10)
```

Assign tier:
- **Platinum (90-100)**: Preferred status, priority DC placement, lower fee structure
- **Gold (80-89)**: Standard terms, meets expectations
- **Silver (70-79)**: Improvement plan required, quarterly review
- **Bronze (< 70)**: Probation — 90-day improvement deadline, risk of termination

### Step 6: Generate the Scorecard

Reference the template in `references/supplier-scorecard-template.md`:

```
# Supplier Scorecard: [Supplier Name]
**Period**: [Month Year]  |  **Tier**: [Platinum / Gold / Silver / Bronze]
**Composite Score**: [0-100]  |  **Prior Month**: [0-100] ([+/- change])

## Distribution Profile
| Metric | Value |
|--------|-------|
| Active SKUs | [N] |
| DCs Stocked | [N] of 55 |
| Product Families | [N] |
| Supplier Since | [date] |

## KPI Performance

| KPI | Weight | Score | Raw Value | Target | Status |
|-----|--------|-------|-----------|--------|--------|
| Fill Rate | 30% | [0-100] | [X]% | > 97% | [Met / Below] |
| OTIF | 25% | [0-100] | [X]% | > 95% | [Met / Below] |
| Shelf-Life | 20% | [0-100] | [X]% | > 99% | [Met / Below] |
| Quality | 15% | [0-100] | [X]% issue rate | < 0.5% | [Met / Below] |
| Responsiveness | 10% | [0-100] | [X] hours avg | < 24 hours | [Met / Below] |

## Trend (Trailing 6 Months)
| Month | Composite | Fill Rate | OTIF | Shelf-Life | Quality | Tier |
|-------|-----------|-----------|------|------------|---------|------|
| [M-5] | ... | ... | ... | ... | ... | ... |
| [M-4] | ... | ... | ... | ... | ... | ... |
| [M-3] | ... | ... | ... | ... | ... | ... |
| [M-2] | ... | ... | ... | ... | ... | ... |
| [M-1] | ... | ... | ... | ... | ... | ... |
| Current | ... | ... | ... | ... | ... | ... |

## Issues and Actions
| Issue | Severity | Root Cause | Corrective Action | Due Date |
|-------|----------|-----------|-------------------|----------|
| ... | ... | ... | ... | ... |

## Recommendations
- [Expand / Maintain / Reduce / Terminate recommendation with rationale]
```

### Step 7: Flag Escalations

- Supplier dropped below Bronze: recommend termination review to Director of Supplier Relations
- Supplier dropped 2+ tiers in one month: immediate escalation — possible systemic issue
- Fill rate below 85%: immediate alert to Director of Supply Chain
- Any quality hold or recall: notify VP Operations immediately
- New supplier below Silver after 90 days: flag for onboarding process review

## Notes

- The `account-deep-dive` MCP prompt provides useful supplier context — invoke it before building the scorecard
- Scorecards are most valuable when trend data is available — a single month snapshot is less actionable than a 6-month trend
- For the complete scorecard template and scoring rubric, see `references/supplier-scorecard-template.md`
- At 10K+ suppliers, batch scorecard generation is essential — individual scorecards are only generated for top suppliers and underperformers
