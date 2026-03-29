---
name: promo-calendar-manager
description: "Track and manage the promotional calendar including TPRs, endcaps, circular features, and seasonal events. Use when planning promotions, checking promo status, or reviewing post-promo performance."
slug: promo-calendar-manager
tags:
  - merchandising
  - promotions
  - trade-funds
  - calendar
---

# Promo Calendar Manager

Track promotional events with timing, vendor funding, pricing, and performance measurement. Manages the full promotional lifecycle from planning through post-promo analysis.

## When to Use

- Weekly promo calendar check (Wednesday 9 AM CT)
- Planning a new promotional event or promotional period
- Checking status of upcoming promotions (funding confirmed? pricing in systems?)
- Reviewing post-promo lift on recently completed events
- Coordinating vendor funding commitments for promotional slots
- User asks to "plan a promo," "check the promo calendar," or "review promo performance"

## Workflow

### Step 1: Identify Promotional Context

Ask the user (if not already provided):
- Are you planning a new promotion, checking existing promos, or reviewing results?
- Which category, product, or vendor?
- What time horizon? (this week, next 4 weeks, next 12 weeks)

### Step 2: For Planning New Promotions

1. **Identify the product**: `mcp__sally-mcp__search_products` and `mcp__sally-mcp__get_product` to pull product details.
2. **Check vendor status**: `mcp__sally-mcp__get_company` and `mcp__sally-mcp__search_accounts` to confirm vendor relationship and account status.
3. **Check vendor pipeline**: `mcp__sally-mcp__search_opportunities` to see if there are existing promotional commitments from this vendor.

Fill in the promotional event template:

```
## Promotional Event
- **Product**: [product name and SKU]
- **Promo type**: [TPR / Endcap / Circular / Sampling / BOGO / Seasonal]
- **Dates**: [start date] — [end date]
- **Regular retail**: $[X]
- **Promo retail**: $[X]
- **Discount %**: [X]%
- **Stores**: [All / Regional: list / Selected: list]

## Vendor Funding
- **Funding type**: [MCB / Off-invoice / Scan deal / Slotting / None]
- **Funding amount**: $[X] per unit or $[X] total
- **Funding confirmed**: [Yes / Pending / No]
- **Funding contact**: [vendor contact name]
- **Submission deadline**: [date for MCB or scan deal claims]

## Expected Performance
- **Baseline units/week**: [X] (last 4 weeks average)
- **Expected promo units/week**: [X]
- **Expected lift**: [X]% vs baseline
- **Trade fund ROI**: Expected incremental margin vs funding cost

## Status
- [ ] Vendor funding confirmed
- [ ] Pricing entered in POS system
- [ ] Display/signage ordered (if endcap or special display)
- [ ] Store communication sent (if store-level execution required)
- [ ] Product inventory confirmed sufficient for promo period
```

4. Track the promotion as an opportunity using `mcp__sally-mcp__create_opportunity` with promotional details in the notes.

### Step 3: For Checking Existing Promotions

1. Pull all promotional opportunities: `mcp__sally-mcp__search_opportunities` filtered by promotional type or date range.
2. For each upcoming promotion, verify:
   - Is vendor funding confirmed?
   - Is pricing in the system?
   - Is inventory sufficient?
   - Are displays/signage ordered?
3. Flag any promotions with unresolved items.

### Step 4: For Reviewing Post-Promo Performance

**Note**: Post-promo lift analysis requires POS data that is NOT currently available via MCP tools. This section describes the target workflow.

For each completed promotion, compile:

```
## Post-Promo Analysis: [Product] — [Promo Type]
**Dates**: [start] — [end]

## Sales Performance
- Baseline units/week (4-week pre-promo average): [X]
- Promo units/week: [X]
- Incremental units/week: [X]
- Lift vs baseline: [X]%

## Financial Performance
- Incremental revenue: $[X]
- Trade fund cost: $[X]
- Incremental margin: $[X]
- Trade fund ROI: [X]:1

## Post-Promo Effect
- Week 1 post-promo units: [X] (pantry loading check)
- Return to baseline by week: [X]

## Verdict
- [Repeat / Modify / Discontinue]
- [Specific notes for next time]
```

### Step 5: Calendar Summary View

Compile a rolling 12-week promotional calendar:

```
# Promotional Calendar — [Date Range]

## This Week (Live)
| Product | Type | Dates | Promo Price | Funding | Status |
|---------|------|-------|-------------|---------|--------|
| ... | ... | ... | ... | ... | Live |

## Next 2 Weeks (Confirmed)
| Product | Type | Dates | Promo Price | Funding | Status |
|---------|------|-------|-------------|---------|--------|
| ... | ... | ... | ... | Confirmed | Ready |

## Weeks 4-12 (Pipeline)
| Product | Type | Dates | Promo Price | Funding | Status |
|---------|------|-------|-------------|---------|--------|
| ... | ... | ... | ... | Pending | Planning |

## Gaps
- [Categories with no promotional coverage in the next 12 weeks]
- [Promotional slots without confirmed vendor funding]
```

## Limitations

- **No dedicated promotional calendar model in MCP**: Promotions are tracked as opportunities, which is a workaround. A purpose-built promo calendar data model would improve this workflow significantly.
- **No POS data for lift analysis**: Post-promo performance analysis requires POS data that is not available via MCP. Must be gathered manually.
- **No trade fund reconciliation**: MCB submissions, scan deal claims, and off-invoice credits must be tracked outside of Satellite.
- **No display compliance tracking**: Endcap and display compliance at store level must be verified through store visits or photo audits, not through MCP.
- **No automated pricing system integration**: Promotional pricing must be manually entered in the retailer's POS system.
