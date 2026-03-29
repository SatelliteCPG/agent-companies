# Supplier Scorecard Template and Scoring Rubric

Reference template for generating monthly supplier performance scorecards at a national CPG distributor.

## Scoring Rubric

Each KPI is scored on a 0-100 scale and then weighted to produce a composite score.

### Fill Rate Scoring (Weight: 30%)

| Raw Fill Rate | Score | Interpretation |
|---------------|-------|----------------|
| >= 99% | 100 | Exceptional — virtually no shorts |
| 98-98.9% | 95 | Excellent — rare shortages |
| 97-97.9% | 90 | Very good — meets target |
| 96-96.9% | 80 | Good — minor issues |
| 95-95.9% | 70 | Acceptable — needs attention |
| 93-94.9% | 55 | Below standard — improvement needed |
| 90-92.9% | 40 | Poor — frequent shorts |
| 85-89.9% | 25 | Critical — impacting retailers |
| < 85% | 10 | Unacceptable — termination risk |

### OTIF Scoring (Weight: 25%)

| Raw OTIF Rate | Score | Interpretation |
|---------------|-------|----------------|
| >= 98% | 100 | Exceptional — nearly perfect delivery |
| 96-97.9% | 90 | Excellent — consistent reliability |
| 95-95.9% | 85 | Very good — meets target |
| 93-94.9% | 70 | Acceptable — occasional misses |
| 90-92.9% | 55 | Below standard — frequent late/incomplete |
| 85-89.9% | 35 | Poor — disrupting fulfillment |
| < 85% | 15 | Unacceptable — unreliable supplier |

### Shelf-Life Compliance Scoring (Weight: 20%)

| Raw Compliance | Score | Interpretation |
|----------------|-------|----------------|
| >= 99.5% | 100 | Exceptional — virtually no short-dated product |
| 99-99.4% | 90 | Excellent — rare occurrences |
| 98-98.9% | 75 | Acceptable — some short-dated receipts |
| 97-97.9% | 60 | Below standard — impacts retailer confidence |
| 95-96.9% | 40 | Poor — regular short-dated product |
| < 95% | 15 | Unacceptable — systematic shelf-life issue |

Short-dated product (< 75% shelf life remaining at receipt) causes:
- Retailer returns and destroy claims
- Markdown pressure
- Consumer complaints
- Potential food safety risks for very short-dated items

### Quality Scoring (Weight: 15%)

| Quality Issue Rate | Score | Interpretation |
|--------------------|-------|----------------|
| < 0.1% | 100 | Exceptional — virtually zero defects |
| 0.1-0.3% | 90 | Excellent — rare issues |
| 0.3-0.5% | 80 | Very good — meets target |
| 0.5-0.8% | 65 | Acceptable — some concerns |
| 0.8-1.0% | 50 | Below standard — consistent quality issues |
| 1.0-2.0% | 30 | Poor — impacting retailer satisfaction |
| > 2.0% | 10 | Unacceptable — systematic quality failure |

Quality issues include:
- Damaged cases or units
- Labeling errors (wrong product, wrong allergen info, missing certifications)
- Product defects (off taste, color, texture)
- Packaging failures (leaks, seal issues)
- Recall events (scored as 0 for that month regardless of rate)

### Responsiveness Scoring (Weight: 10%)

| Avg Response Time | Score | Interpretation |
|-------------------|-------|----------------|
| < 4 hours | 100 | Exceptional — immediate response |
| 4-12 hours | 90 | Excellent — same business day |
| 12-24 hours | 80 | Very good — next business day |
| 24-48 hours | 60 | Acceptable — within 2 days |
| 48-72 hours | 40 | Below standard — slow response |
| > 72 hours | 15 | Unacceptable — unresponsive |

## Tier Definitions

### Platinum (Composite 90-100)
- **Benefits**: Preferred DC placement priority, lower promotional fees, featured in retailer recommendations, first access to new DC openings, expedited item setup
- **Review cadence**: Annually
- **Typical supplier profile**: Top 5% of suppliers, consistent 12+ months of high performance

### Gold (Composite 80-89)
- **Benefits**: Standard terms, full DC access, standard promotional rates
- **Review cadence**: Semi-annually
- **Typical supplier profile**: Reliable suppliers meeting all expectations consistently

### Silver (Composite 70-79)
- **Requirements**: Formal improvement plan within 30 days, quarterly performance reviews
- **Restrictions**: No DC expansion until back to Gold, higher scrutiny on new item requests
- **Typical supplier profile**: Suppliers with 1-2 KPIs below target, recoverable with focused effort

### Bronze (Composite < 70)
- **Requirements**: 90-day improvement deadline, monthly performance reviews, senior supplier contact engaged
- **Restrictions**: No new items, no DC expansion, potential DC reduction
- **Escalation**: 2 consecutive months of Bronze triggers termination review
- **Typical supplier profile**: Suppliers with systemic performance issues across multiple KPIs

## Batch Processing Notes

At 10K+ suppliers, monthly scorecard generation is a batch process:

1. **Automated scoring**: Composite scores calculated from ERP/WMS data exports for all active suppliers
2. **Tier assignment**: Automatic tier assignment based on composite score
3. **Exception flagging**: Automatic identification of tier changes, threshold breaches, and trending declines
4. **Individual scorecards**: Generated only for:
   - Top 100 suppliers (by revenue)
   - All suppliers below Gold tier
   - Any supplier with a tier change
   - Suppliers flagged for review by other teams
5. **Summary report**: Aggregate tier distribution, average scores by category, and exception list for Director of Supplier Relations

## Data Integration Notes

- **Available via MCP**: Supplier profile (`search_accounts`, `get_company`), product catalog (`search_products`), distribution footprint (`get_distributor_codes`, `search_distribution_centers`), contact information (`search_contacts`)
- **Not available via MCP (required from ERP/WMS)**: Fill rate, OTIF, shelf-life compliance, quality issue rates, detailed order/receipt history
- **Gap impact**: MCP tools provide the "who and what" (supplier identity, products, DCs) but not the "how well" (operational performance). Scorecard generation requires both.
