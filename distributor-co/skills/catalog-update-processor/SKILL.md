---
name: catalog-update-processor
description: "Process a batch of product catalog updates including new item setups, attribute changes, price updates, and discontinuations with GS1 validation. Use when processing catalog changes or reviewing data quality."
slug: catalog-update-processor
tags:
  - catalog
  - products
  - data-quality
  - gs1
---

# Catalog Update Processor

Process batch product catalog updates — new item setups, attribute changes, price changes, and discontinuations — with GS1 validation rules. Designed for distributors managing millions of SKUs with hundreds of daily catalog changes.

## When to Use

- Weekly catalog update cycle (Wednesday processing)
- User submits a batch of product changes from a supplier
- User asks to set up new items in the catalog
- User asks to validate product data quality
- User asks to process price changes
- User asks to discontinue products

## Workflow

### Step 1: Identify the Update Type

Ask the user (if not already provided):
- What type of update? (New items, attribute changes, price changes, discontinuations, or mixed batch)
- Which supplier?
- How many items?
- Source of the data? (Supplier submission, internal audit, system migration)

### Step 2: Validate Input Data

For each item in the batch, validate against GS1 rules (see `references/gs1-validation-rules.md`):

#### GTIN Validation
1. Check format: GTIN-12 (UPC-A) for retail units, GTIN-14 for case-level codes
2. Verify check digit using the standard modulo-10 algorithm
3. Verify company prefix is registered (cross-reference with GS1 registry if available)
4. Check for duplicates: Call `mcp__sally-mcp__search_products` to see if GTIN already exists in the catalog
5. No MCP tool for GS1 registry lookup yet — manual verification against GS1's GEPIR database

#### Required Fields Validation
Check that all required fields are present and properly formatted:

| Field | Format | Required |
|-------|--------|----------|
| GTIN/UPC | GTIN-12 or GTIN-14 | Yes |
| Product description | Max 200 chars, no special characters | Yes |
| Brand name | As registered | Yes |
| Case pack configuration | Integer (units per case) | Yes |
| Inner pack count | Integer (units per inner pack) | If applicable |
| Unit dimensions (H x W x D) | Decimal inches | Yes |
| Unit weight | Decimal ounces or pounds | Yes |
| Case dimensions (H x W x D) | Decimal inches | Yes |
| Case weight | Decimal pounds | Yes |
| Pallet configuration (Ti x Hi) | Integer x Integer | Yes |
| Shelf life | Integer days | Yes |
| Temperature class | Ambient / Refrigerated / Frozen | Yes |
| Country of origin | ISO 3166-1 alpha-2 | Yes |
| Certifications | Organic, Non-GMO, Kosher, etc. | If applicable |

### Step 3: Process by Update Type

#### New Item Setup
1. Validate all fields pass GS1 and completeness rules
2. Check for duplicates: `mcp__sally-mcp__search_products` by GTIN and product name
3. Verify the supplier account exists: `mcp__sally-mcp__search_accounts`
4. Note: `mcp__sally-mcp__update_product` handles single-item updates. No bulk creation tool yet — at distributor scale, new item batches of 50-200 items require system-level import.
5. For each item, document: GTIN, description, category assignment, initial pricing, target DC allocation
6. Hand off DC allocation to Inventory Planner

#### Attribute Changes
1. Retrieve existing product record: `mcp__sally-mcp__get_product`
2. Validate changed fields against GS1 rules
3. Check if changes require a new GTIN:
   - **New GTIN required**: Net weight change > 20%, product reformulation, new pack size
   - **Same GTIN OK**: Minor description update, certification addition/removal, packaging material change
4. Apply changes: `mcp__sally-mcp__update_product` for individual items
5. If dimensions or weight changed, notify DC Operations Manager (affects warehouse slotting)

#### Price Changes
1. Retrieve current pricing: `mcp__sally-mcp__get_product` for current cost/price
2. Calculate margin impact: (new cost - old cost) / old cost
3. Flag significant changes (> 5% increase or any decrease) for Director of Catalog & Pricing review
4. Apply approved changes with effective date
5. Notify Pricing Analyst for downstream pricing updates (retail pricing, promotional adjustments)

#### Discontinuations
1. Verify the product exists and is currently active: `mcp__sally-mcp__get_product`
2. Check DC stocking status: `mcp__sally-mcp__get_distributor_codes` — verify inventory levels before deactivating
3. Coordinate sell-through timeline with Inventory Planner
4. Notify Retail Account Manager for accounts that regularly order the product
5. Schedule code deactivation at each DC after inventory is cleared
6. Archive the product record

### Step 4: Generate Processing Report

```
# Catalog Update Report — [Date]

## Batch Summary
| Update Type | Submitted | Passed Validation | Failed Validation | Processed |
|-------------|-----------|-------------------|-------------------|-----------|
| New Items | [N] | [N] | [N] | [N] |
| Attribute Changes | [N] | [N] | [N] | [N] |
| Price Changes | [N] | [N] | [N] | [N] |
| Discontinuations | [N] | [N] | [N] | [N] |
| **Total** | [N] | [N] | [N] | [N] |

## Validation Failures
| Item | GTIN | Issue | Resolution |
|------|------|-------|------------|
| ... | ... | Invalid check digit | Correct GTIN |
| ... | ... | Missing shelf life | Request from supplier |
| ... | ... | Duplicate GTIN | Verify — same product or data error? |

## Items Requiring Approval
| Item | GTIN | Change | Reason for Review |
|------|------|--------|-------------------|
| ... | ... | Cost increase > 5% | Director approval needed |
| ... | ... | New GTIN required | Reformulation — verify with supplier |

## DC Impact
| Item | Change | Affected DCs | Action Required |
|------|--------|-------------|-----------------|
| ... | Dimension change | [N] DCs | Update warehouse slotting |
| ... | Discontinuation | [N] DCs | Sell-through and deactivation |

## Data Quality Metrics
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Completeness rate | [X]% | [X]% | [+/-] |
| GS1 compliance rate | [X]% | [X]% | [+/-] |
| Items with missing fields | [N] | [N] | [+/-] |
```

### Step 5: Post-Processing Notifications

After processing, notify relevant teams:
- **DC Operations Manager**: If dimension/weight changes affect warehouse slotting
- **Pricing Analyst**: If price changes need downstream retail pricing updates
- **Inventory Planner**: If new items need DC allocation and safety stock
- **Retail Account Manager**: If discontinuations affect active retail accounts
- **Director of Catalog & Pricing**: Summary report with quality metrics

## Notes

- The `search_products` and `update_product` MCP tools handle individual item operations. At distributor scale (hundreds of changes per day), most catalog processing happens through batch import systems. Skills describe the workflow; bulk execution requires system-level tools not yet in MCP.
- GS1 validation rules are detailed in `references/gs1-validation-rules.md`
- Price changes should never go live without margin analysis — even a small cost increase on a high-volume SKU has material P&L impact
- Discontinuations are the highest-risk catalog change — they affect live retailer ordering. Always verify inventory is cleared before deactivating codes.
