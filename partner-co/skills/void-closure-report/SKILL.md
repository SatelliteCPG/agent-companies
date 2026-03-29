---
name: void-closure-report
description: "Compare authorized items against distributor DC stocking to surface gaps. Use during weekly void reviews or when tracking authorization-to-shelf closure across the brand portfolio."
slug: void-closure-report
tags:
  - distribution
  - voids
  - reporting
  - multi-brand
---

# Void Closure Report

Generate a structured gap analysis comparing authorized items against distributor DC stocking data. Surfaces products that are authorized at retailers but not flowing through distribution — the "void" between authorization and shelf presence.

## When to Use

- Weekly void status check (typically Monday)
- After a new retail authorization is won — to verify distribution follow-through
- User asks about "voids," "gaps," or "authorized but not stocked"
- Before buyer meetings to confirm products are actually available at the retailer's DCs
- When brand principals ask about distribution execution

## Workflow

### Step 1: Define Scope

Ask the user (if not already clear):
- All brands or a specific brand?
- All retailers or a specific retailer?
- All distributors or a specific distributor (UNFI, KeHE)?

### Step 2: Pull Authorization Data

1. Call `mcp__sally-mcp__get_distributor_codes` to get all active product-distributor code mappings
2. Call `mcp__sally-mcp__get_distributor_families` to see which product families are authorized at which DCs
3. Call `mcp__sally-mcp__search_distribution_centers` to get the full DC list with metadata

### Step 3: Pull Product Catalog

1. Call `mcp__sally-mcp__search_products` to get the full product catalog across all brands
2. Map each product to its brand and product family
3. Note expected DC coverage for each product based on retailer targets

### Step 4: Build the Authorization Matrix

Create a product-by-DC matrix showing authorization status:
- **Authorized and active**: Product is set up and flowing through the DC
- **Authorized but inactive**: Code exists but no movement detected
- **Not authorized**: Product has no code at this DC
- **Pending**: Authorization submitted but not yet confirmed

### Step 5: Identify Voids

A void exists when:
1. A product has been authorized by a retailer buyer (opportunity closed-won)
2. The retailer's serving DC does not have the product authorized or active
3. OR the DC has the product authorized but it is not flowing (inactive code)

Cross-reference with `mcp__sally-mcp__search_opportunities` to find closed-won opportunities and verify DC follow-through.

### Step 6: Compile the Void Report

```
# Void Closure Report — [Date]

## Summary
- Total product-DC combinations tracked: [N]
- Authorized and active: [N] ([X]%)
- Voids identified: [N] ([X]%)
- Voids closed this period: [N]
- Net change: [+/-N]

## Voids by Brand (sorted by void count)
| Brand | Products Authorized | Active | Voids | Void Rate | Revenue Impact |
|-------|-------------------|--------|-------|-----------|---------------|
| [Brand 1] | [N] | [N] | [N] | [X]% | $[est] |
| [Brand 2] | [N] | [N] | [N] | [X]% | $[est] |
| ...   | ...               | ...    | ...   | ...       | ...           |

## Voids by Retailer (sorted by void count)
| Retailer | Brands Affected | Products Voided | Serving DC | Status |
|----------|----------------|-----------------|------------|--------|
| [Retailer 1] | [N] | [list] | [DC name] | [action needed] |
| ...      | ...            | ...             | ...        | ...    |

## Void Detail
| Brand | Product | Retailer | DC | Authorization Date | Days Voided | Action |
|-------|---------|----------|----|--------------------|-------------|--------|
| ...   | ...     | ...      | ...| ...                | ...         | ...    |

## Closures This Period
| Brand | Product | Retailer | DC | Void Duration | How Closed |
|-------|---------|----------|----|----|------------|
| ...   | ...     | ...      | ...| [N] days | [action taken] |

## Priority Actions
1. [Highest revenue impact void — specific action]
2. [Longest-standing void — specific action]
3. [Void blocking active opportunity — specific action]
```

### Step 7: Generate Closure Actions

For each void, recommend a specific closure action:
- **DC code inactive**: Contact distributor to reactivate. Use `distributor-check` MCP prompt.
- **DC not authorized**: Submit authorization request to DC. Coordinate with Director of Operations.
- **Inventory issue**: DC authorized but out of stock. Escalate to brand principal for fill rate attention.
- **Retailer order issue**: DC stocked but retailer not ordering. Coordinate with Broker Sales Rep to contact buyer.

## Notes

- Void closure is a lagging indicator — it can take 2-4 weeks from authorization to shelf
- Factor in lead times before flagging a fresh authorization as a void
- Revenue impact is estimated based on product retail price and estimated velocity — not exact
- This report pairs with `partner-pipeline-dashboard` to show the full picture: pipeline to authorization to shelf
