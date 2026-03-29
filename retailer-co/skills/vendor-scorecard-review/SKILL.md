---
name: vendor-scorecard-review
description: "Pull vendor performance data and generate a formatted scorecard with fill rate, delivery, quality, and promotional metrics. Use during weekly vendor reviews or when evaluating vendor tier status."
slug: vendor-scorecard-review
tags:
  - vendor-relations
  - compliance
  - scorecards
  - analytics
---

# Vendor Scorecard Review

Pull vendor/supplier data and format into a standardized scorecard template with performance metrics and trend analysis. Designed for the weekly vendor compliance review cadence.

## When to Use

- Weekly vendor scorecard review (Monday 9 AM CT)
- Evaluating a vendor for tier upgrade or downgrade
- Preparing for category reviews that include vendor performance assessment
- Investigating a vendor compliance issue or escalation
- Onboarding review at 90 days for new vendors

## Workflow

### Step 1: Identify the Vendor

Ask the user (if not already provided):
- Which vendor or vendor list?
- Review period (default: last 4 weeks)
- Any specific metrics to focus on?

Pull vendor data:

1. **Vendor profile**: `mcp__sally-mcp__get_company` with the vendor name
2. **Account details**: `mcp__sally-mcp__search_accounts` for the vendor account record
3. **Contact roster**: `mcp__sally-mcp__search_contacts` filtered to the vendor
4. **Product families**: `mcp__sally-mcp__list_account_families` to see products associated with this vendor
5. **Distribution status**: `mcp__sally-mcp__get_distributor_codes` and `mcp__sally-mcp__get_distributor_families` for DC authorization

### Step 2: Gather Performance Metrics

**Note**: Most vendor performance metrics (fill rate, OTIF, quality incidents) are NOT currently available via MCP tools. This section describes the target workflow. Currently, these metrics must be gathered manually from supply chain systems, warehouse reports, or vendor-provided data.

Metrics to gather:

| Metric | Source | MCP Tool Available? |
|--------|--------|-------------------|
| Fill rate | Warehouse/DC receiving logs | No — manual pull |
| On-time delivery | Delivery timestamps vs PO dates | No — manual pull |
| Shelf-life at receipt | Receiving inspection records | No — manual pull |
| Quality incidents | Quality team reports | No — manual pull |
| Promo execution | Promo compliance checks | No — manual pull |
| Product catalog | Satellite product database | Yes — `search_products` |
| Account history | Satellite CRM | Yes — `search_accounts` |
| Pipeline activity | Satellite CRM | Yes — `search_opportunities` |

### Step 3: Score Against Targets

Apply the scorecard thresholds from `references/vendor-scorecard-template.md`:

| Metric | Target | Warning | Critical |
|--------|--------|---------|----------|
| Fill rate | 97%+ | 95-97% | <95% |
| On-time delivery | 95%+ | 90-95% | <90% |
| Shelf-life at receipt | 75%+ remaining | 60-75% | <60% |
| Quality incidents | 0/quarter | 1/quarter | 2+/quarter |
| Promo execution | 95%+ | 85-95% | <85% |

### Step 4: Compile the Scorecard

```
# Vendor Scorecard: [Vendor Name]
**Review period**: [start date] — [end date]
**Reviewer**: Vendor Compliance Manager
**Vendor tier**: [Preferred / Standard / Probation / New]

## Performance Summary
| Metric | Target | Actual | Status | Trend |
|--------|--------|--------|--------|-------|
| Fill Rate | 97%+ | [X]% | [Green/Yellow/Red] | [Up/Down/Flat] |
| On-Time Delivery | 95%+ | [X]% | [Green/Yellow/Red] | [Up/Down/Flat] |
| Shelf-Life Compliance | 75%+ | [X]% | [Green/Yellow/Red] | [Up/Down/Flat] |
| Quality Incidents | 0/qtr | [X] | [Green/Yellow/Red] | [Up/Down/Flat] |
| Promo Execution | 95%+ | [X]% | [Green/Yellow/Red] | [Up/Down/Flat] |

## Overall Score: [X/5 metrics at target]

## Products Supplied
| Product | Category | Velocity | Margin | DC Status |
|---------|----------|----------|--------|-----------|
| ... | ... | ... | ... | ... |

## Incidents / Issues
[List any specific incidents during the review period]

## Trend Analysis
[4-week or 4-month trend for each metric — improving, stable, or deteriorating]

## Action Required
- [Specific actions: none / vendor notification / improvement plan / escalation]
- [Timeline for next review]

## Vendor Contact
| Name | Title | Email | Phone |
|------|-------|-------|-------|
| ... | ... | ... | ... |
```

### Step 5: Determine Actions

Based on scorecard results:

- **All green**: No action needed. Continue standard monitoring.
- **Any yellow**: Send vendor notification with specific metric and 30-day improvement target.
- **Any red**: Issue formal improvement plan. Notify Director of Vendor Relations. 14-day review.
- **Multiple red**: Escalate to VP Merchandising. Begin sourcing alternatives.
- **New vendor at 90 days**: Formal go/no-go decision. Pass to standard monitoring or terminate.

## Limitations

- **~80% of scorecard data requires manual input**: Fill rate, OTIF, quality, and promo execution data are not in Satellite's MCP tools. This skill describes the target workflow but currently depends on manual data gathering from supply chain systems.
- **No automated trend tracking**: Scorecard history must be maintained manually or in spreadsheets until a vendor scorecard data model is available.
- **No automated vendor notifications**: Improvement plan notifications must be sent manually via email.
