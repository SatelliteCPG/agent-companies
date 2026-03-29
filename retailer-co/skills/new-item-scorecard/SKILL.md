---
name: new-item-scorecard
description: "Evaluate a new product submission from a vendor or broker using a structured scoring rubric. Use when reviewing vendor product pitches, processing new item submissions, or preparing for category reviews."
slug: new-item-scorecard
tags:
  - vendor-relations
  - evaluation
  - new-items
  - category-management
---

# New Item Scorecard

Evaluate a new product submission from a vendor or broker using a structured scoring rubric. Produces a standardized scorecard with scores across four dimensions: margin, category fit, differentiation, and supplier readiness.

## When to Use

- A vendor or broker submits a new product for consideration
- User asks to "evaluate," "score," or "review" a product submission
- During weekly new item review sessions
- When preparing new item recommendations for category reviews
- When comparing multiple competing submissions for the same shelf slot

## Workflow

### Step 1: Gather Product Information

Ask the user (if not already provided):
- Product name and brand
- Category and subcategory
- Suggested retail price and wholesale cost
- Pack size and case pack

Then pull available data:

1. **Check for existing products**: `mcp__sally-mcp__search_products` — does this product or a similar SKU already exist in the catalog?
2. **Pull sellsheet**: `mcp__sally-mcp__get_sellsheet` or `mcp__sally-mcp__search_sellsheets` — review vendor-submitted materials for completeness
3. **Vendor profile**: `mcp__sally-mcp__get_company` and `mcp__sally-mcp__search_accounts` — pull vendor track record, existing relationship, account status

### Step 2: Score Using the Rubric

Score each dimension 0-5 using the criteria in `references/new-item-evaluation-rubric.md`:

#### Margin (0-5)
- 5: Margin exceeds category average by 5%+
- 4: Margin exceeds category average by 2-5%
- 3: Margin meets category average
- 2: Margin below category average but above minimum threshold
- 1: Margin at minimum threshold
- 0: Margin below minimum threshold

#### Category Fit (0-5)
- 5: Fills a documented consumer need with no current offering
- 4: Addresses underserved segment with limited current offerings
- 3: Adds variety to a segment with adequate coverage
- 2: Overlaps with existing items but offers minor differentiation
- 1: Largely duplicates an existing item with marginal difference
- 0: Direct duplicate of existing item — no incremental value

#### Differentiation (0-5)
- 5: Genuinely novel formulation, format, or positioning — first-to-market
- 4: Strong differentiation through unique ingredients, process, or brand story
- 3: Meaningful differentiation vs existing set (better taste, cleaner label, strong brand)
- 2: Minor differentiation (different flavor, slightly different positioning)
- 1: Me-too product with packaging as primary differentiator
- 0: No meaningful differentiation from existing shelf set

#### Supplier Readiness (0-5)
- 5: Established vendor, 97%+ fill rate, national DC authorization, proven scale
- 4: Established vendor, 95%+ fill rate, regional DC authorization
- 3: Growing vendor, reliable track record, DC authorization in progress
- 2: Early-stage vendor, limited DC authorization, some track record
- 1: Startup vendor, no DC authorization, untested fulfillment
- 0: Pre-revenue or pre-production — cannot currently fulfill orders

### Step 3: Calculate Total and Route

| Total Score | Tier | Action |
|-------------|------|--------|
| 16-20 | Fast Track | Route to category manager immediately. High-potential item. |
| 11-15 | Standard | Route to category manager with scorecard for review at next cycle. |
| 6-10 | Waitlist | Notify vendor of gaps. Invite resubmission after improvements. |
| 0-5 | Decline | Send standard decline with specific feedback on weakest dimensions. |

### Step 4: Compile the Scorecard

```
# New Item Scorecard: [Product Name]
**Brand**: [brand]  |  **Category**: [category]
**Submitted by**: [vendor/broker name]  |  **Date**: [date]

## Scores
| Dimension | Score | Notes |
|-----------|-------|-------|
| Margin | [0-5] | [specific reasoning] |
| Category Fit | [0-5] | [specific reasoning] |
| Differentiation | [0-5] | [specific reasoning] |
| Supplier Readiness | [0-5] | [specific reasoning] |
| **Total** | **[0-20]** | **[tier: Fast Track / Standard / Waitlist / Decline]** |

## Product Details
- Suggested retail: $[X]
- Wholesale cost: $[X]
- Estimated margin: [X]%
- Pack size: [X]
- Certifications: [organic, non-GMO, etc.]

## Existing Shelf Set
[List 2-3 most similar products currently on shelf with their velocity data if available]

## Recommendation
[1-2 sentences: specific recommendation and reasoning]

## Gaps / Risks
- [Any missing information from the vendor]
- [Supply chain concerns]
- [Competitive risks]
```

### Step 5: Log and Track

1. Create or update the pipeline opportunity using `mcp__sally-mcp__create_opportunity` or `mcp__sally-mcp__update_opportunity` with the evaluation result.
2. If routed to category manager, note which category manager and the routing date.
3. If declined or waitlisted, ensure vendor communication is sent.

## Limitations

- **No automated margin calculation**: Margin thresholds must be provided by the user or referenced from category standards. No MCP tool currently calculates margin from cost/retail inputs.
- **No syndicated data comparison**: Cannot automatically benchmark against market velocity or share data. Syndicated data context must be provided manually.
- **No submission intake form**: Submissions arrive via email, broker meetings, or trade shows. No structured intake workflow in MCP.
- **No cross-submission comparison**: Cannot currently display side-by-side comparisons of competing submissions for the same slot.
