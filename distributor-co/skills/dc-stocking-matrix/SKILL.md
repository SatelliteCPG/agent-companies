---
name: dc-stocking-matrix
description: "Generate a product-by-DC stocking matrix showing which products are stocked at which distribution centers. Use when reviewing DC allocation, identifying coverage gaps, or planning inventory distribution."
slug: dc-stocking-matrix
tags:
  - supply-chain
  - distribution
  - inventory
  - allocation
---

# DC Stocking Matrix

Generate a product-by-DC allocation matrix showing which products are stocked at which distribution centers across the network. Identifies coverage gaps, velocity mismatches, and allocation optimization opportunities. Designed for a distributor operating 55+ DCs.

## When to Use

- User asks which DCs stock a specific product
- User asks about DC coverage or stocking gaps
- User wants to review product allocation across the network
- Before allocating a new product to DCs
- When investigating fill rate issues that may be allocation-related
- During quarterly DC allocation reviews

## Workflow

### Step 1: Determine Scope

Ask the user (if not already provided):
- Specific products/product families, or the full catalog?
- Specific DCs/regions, or the full network?
- Is this a routine review or investigating a specific issue?

### Step 2: Pull DC Network Data

1. Call `mcp__sally-mcp__search_distribution_centers` to get all DCs in scope with their locations and regions
2. Call `mcp__sally-mcp__list_distributors` to get distributor-level overview
3. Note DC attributes: region, size classification, temperature capability (ambient, refrigerated, frozen)

### Step 3: Pull Product and Code Data

1. Call `mcp__sally-mcp__search_products` for products in scope — get GTIN, name, category, temperature class
2. Call `mcp__sally-mcp__get_distributor_codes` for each product to see which DCs have active codes
3. Call `mcp__sally-mcp__get_distributor_families` to understand product family groupings
4. Call `mcp__sally-mcp__get_product` for detailed attributes on flagged items

### Step 4: Build the Stocking Matrix

Construct a matrix with Products (rows) and DCs (columns):

```
# DC Stocking Matrix — [Date]

## Scope: [product family / category / all] at [region / all DCs]

### Coverage Summary
| Metric | Value |
|--------|-------|
| Products in scope | [N] |
| DCs in scope | [N] |
| Total product-DC slots | [products x DCs] |
| Slots stocked | [N] (X%) |
| Slots not stocked | [N] (X%) |

### Stocking Matrix

| Product | GTIN | Category | East DC1 | East DC2 | Central DC1 | ... | West DC1 |
|---------|------|----------|----------|----------|-------------|-----|----------|
| Product A | 123... | Grocery | Active | Active | Active | ... | -- |
| Product B | 456... | Frozen | Active | -- | Pending | ... | Active |
| Product C | 789... | Refrigerated | -- | -- | Active | ... | -- |
```

Code status values:
- **Active**: Product stocked and available for ordering
- **Pending**: Code created but inventory not yet received
- **Inactive**: Previously stocked, currently deactivated
- **--**: Not authorized at this DC

### Step 5: Identify Gaps

Analyze the matrix for three types of gaps:

**Gap Type 1 — Product not stocked in a region**
- Product is stocked in some regions but has zero DCs in another region
- Impact: Retailers in that region cannot order the product
- Action: Evaluate demand in the region — if retailer demand exists, allocate to a DC

**Gap Type 2 — Partial coverage within a region**
- Product is stocked at some DCs in a region but not all
- May be intentional (low-velocity product consolidated at fewer DCs) or a gap
- Action: Check velocity at stocked DCs — if above threshold, expand to missing DCs

**Gap Type 3 — Code status issues**
- Active products with pending or inactive codes at allocated DCs
- Impact: Orders placed but unable to be fulfilled from expected DC
- Action: Follow up on code activation — pending > 30 days needs investigation

**Gap Type 4 — Velocity mismatch**
- Product stocked at a DC but not meeting minimum velocity threshold
- Impact: Inventory carrying cost exceeds the value of having the product at that DC
- Action: Consider redistribution to higher-velocity DC or consolidation
- Note: Velocity data comes from ERP/WMS — no MCP tool for this yet

### Step 6: Generate Recommendations

```
## Coverage Gaps

### Priority Gaps (retailer demand exists)
| Product | Missing Region/DC | Retailer Demand Signal | Recommended Action |
|---------|-------------------|----------------------|-------------------|
| ... | ... | ... | Allocate to [DC] |

### Code Issues
| Product | DC | Code Status | Days in Status | Action |
|---------|-----|-------------|----------------|--------|
| ... | ... | Pending | [N] | Follow up with DC ops |

### Optimization Opportunities
| Product | DC | Issue | Recommendation |
|---------|-----|-------|---------------|
| ... | ... | Below velocity threshold | Consolidate to [DC] |
| ... | ... | Overstocked | Reduce safety stock |
```

### Step 7: Cross-Reference with Retail Accounts

For identified gaps, check whether retail accounts are affected:

1. Call `mcp__sally-mcp__search_accounts` to find retailers in the gap region
2. Call `mcp__sally-mcp__list_account_families` to check if those retailers order the affected product family
3. Prioritize gap closure where retailers are actively ordering or requesting the product

## Notes

- The `distributor-check` MCP prompt provides a useful starting point for DC status queries — invoke it if available
- At 55+ DCs and millions of SKUs, full-network matrices are impractical to display — always scope to a product family, category, or region
- Velocity thresholds vary by category: shelf-stable items may have lower minimums than refrigerated/frozen
- For detailed DC and distributor management context, see `references/dc-allocation-guide.md`
