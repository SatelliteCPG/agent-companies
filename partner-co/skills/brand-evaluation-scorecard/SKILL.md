---
name: brand-evaluation-scorecard
description: "Structured intake for evaluating whether to take on a new brand client. Use when a prospective brand approaches the broker for representation."
slug: brand-evaluation-scorecard
tags:
  - client-services
  - onboarding
  - evaluation
---

# Brand Evaluation Scorecard

Evaluate whether a prospective brand is a good fit for the broker's portfolio. Produces a structured scorecard with ratings across key dimensions — margin structure, retailer fit, distribution readiness, category demand, and portfolio synergy.

## When to Use

- A new brand approaches the broker about representation
- User asks to "evaluate" or "score" a prospective brand
- During portfolio planning to assess brand fit
- When Managing Partner requests a recommendation on a new brand inquiry

## Workflow

### Step 1: Gather Brand Information

Ask the user (if not already provided):
- Brand name and company
- Product line (categories, SKU count, pack sizes)
- Current distribution (which distributors, which DCs)
- Current retail presence (which retailers, how many stores)
- Commission structure and margin expectations
- Why they are seeking broker representation

If a company record exists, call `mcp__sally-mcp__search_accounts` or `mcp__sally-mcp__get_company` to pull existing data.

### Step 2: Assess Retailer Fit

1. Call `mcp__sally-mcp__search_accounts` to get the broker's active retailer accounts
2. Match the brand's target retailers against the broker's retailer relationships
3. Score:
   - **Strong Fit (4-5)**: Brand's target retailers overlap 70%+ with broker's active accounts
   - **Moderate Fit (2-3)**: 40-70% overlap
   - **Weak Fit (0-1)**: Below 40% overlap

### Step 3: Assess Distribution Readiness

1. Call `mcp__sally-mcp__search_distribution_centers` to check if the brand's products are already set up at relevant DCs
2. Call `mcp__sally-mcp__get_distributor_codes` if any existing codes are in the system
3. Score:
   - **Ready (4-5)**: Products already at UNFI/KeHE with active codes at 70%+ of relevant DCs
   - **Partial (2-3)**: Some DC coverage but gaps in key regions
   - **Not Ready (0-1)**: No distributor setup or minimal coverage

### Step 4: Assess Portfolio Synergy

1. Call `mcp__sally-mcp__search_products` to compare the prospective brand's products against existing portfolio brands
2. Evaluate:
   - Does this brand complement existing brands (different price tier, format, occasion)?
   - Does it compete directly with a current client?
   - Does it fill a category gap in the portfolio?
3. Score:
   - **High Synergy (4-5)**: Fills a gap, no conflicts, enhances portfolio story
   - **Moderate (2-3)**: Some overlap but differentiated enough
   - **Conflict (0-1)**: Directly competes with existing client

### Step 5: Assess Margin Structure

Evaluate the proposed commission and margin:
- What is the broker commission rate?
- What is the estimated revenue potential (# of target retailers x avg order value x frequency)?
- Does the revenue justify the rep time required?
- Score:
  - **Attractive (4-5)**: Above-average commission, strong revenue potential
  - **Standard (2-3)**: Market-rate commission, moderate revenue
  - **Below Threshold (0-1)**: Low commission or limited revenue potential

### Step 6: Assess Category Demand

Evaluate category trends:
- Is this category growing, stable, or declining?
- Is there retailer demand for new products in this category?
- Are competitors exiting or entering?
- Score:
  - **High Demand (4-5)**: Growing category, active retailer interest
  - **Stable (2-3)**: Mature category, replacement opportunities
  - **Low Demand (0-1)**: Declining category, saturated shelf sets

### Step 7: Generate the Scorecard

```
# Brand Evaluation Scorecard: [Brand Name]
**Date**: [date]  |  **Evaluated by**: [name]

## Brand Overview
- **Company**: [name]
- **Categories**: [list]
- **SKU Count**: [N]
- **Current Retail**: [list of current retailers]
- **Current Distribution**: [list of distributors and DCs]

## Evaluation Scores

| Dimension | Score (0-5) | Notes |
|-----------|-------------|-------|
| Retailer Fit | [X] | [brief explanation] |
| Distribution Readiness | [X] | [brief explanation] |
| Portfolio Synergy | [X] | [brief explanation] |
| Margin Structure | [X] | [brief explanation] |
| Category Demand | [X] | [brief explanation] |
| **Overall** | **[avg]** | |

## Recommendation
[ACCEPT / CONDITIONAL / DECLINE]

[2-3 sentences explaining the recommendation]

## Conditions (if conditional)
- [Condition 1 — e.g., "Brand must complete UNFI setup before onboarding"]
- [Condition 2 — e.g., "Commission rate must be renegotiated to X%"]

## Onboarding Requirements (if accepted)
1. CRM setup — company, contacts, products
2. Distributor code verification
3. Sellsheet collection
4. Rep assignment
5. Kickoff meeting scheduling
```

## Decision Framework

See `references/brand-evaluation-criteria.md` for scoring rubric details.

| Overall Score | Recommendation |
|---------------|---------------|
| 4.0-5.0 | **Accept** — Strong fit, proceed to onboarding |
| 3.0-3.9 | **Conditional** — Accept with specific conditions that must be met |
| 2.0-2.9 | **Decline (revisit)** — Not ready now, but could be in 6-12 months |
| 0-1.9 | **Decline** — Poor fit, do not pursue |

## Notes

- Portfolio conflicts are the hardest dimension — never take on a brand that directly competes with a top-performing client without explicit Managing Partner approval
- Distribution readiness is the most common blocker — brands often approach brokers before they have distributor setup complete
- Revenue potential should account for ramp time — first 6 months will have limited pipeline
- Use the `email-to-crm-upsert` MCP prompt to capture initial brand inquiry details from email
