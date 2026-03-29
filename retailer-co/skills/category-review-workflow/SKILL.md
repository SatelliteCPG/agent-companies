---
name: category-review-workflow
description: "Guide a category through the 8-step category management process with data templates and milestone tracking. Use when initiating or executing a category review."
slug: category-review-workflow
tags:
  - category-management
  - reviews
  - strategy
  - assortment
---

# Category Review Workflow

Guide a category through the 8-step category management process — the industry-standard framework for managing retail categories. Provides data templates, milestone tracking, and structured decision points at each step.

## When to Use

- Quarterly category review kickoff
- User asks to "run a category review" or "start category management process"
- When a category is underperforming and needs a full strategic reset
- When onboarding a new category or major category restructuring
- Annual planning that requires category-level strategy setting

## Workflow

### Step 1: Define the Category

**Objective**: Establish what products belong in the category and how consumers think about it.

Gather information:
1. Pull all products in the category using `mcp__sally-mcp__search_products` with category filters.
2. Review the current product set — does it match how consumers shop the category?
3. Consider sub-categories and segments (e.g., "Plant-Based Milk" within "Milk Alternatives").

**Deliverable**: Category definition document listing all products, sub-segments, and consumer decision tree.

**Milestone**: Category definition approved by Director of Category Management.

### Step 2: Assign the Category Role

**Objective**: Determine the category's strategic role for the retailer.

| Role | Definition | Implication |
|------|-----------|-------------|
| Destination | Drives store choice — consumers choose your store for this category | Maximum assortment, competitive pricing, prime shelf space |
| Routine | Regular purchase, expected to be in stock | Standard assortment, market-competitive pricing |
| Seasonal | Driven by time of year or events | Flexible assortment, promotional focus during peaks |
| Convenience | Fill-in purchase, not a trip driver | Limited assortment, standard margins |

**Deliverable**: Category role assignment with supporting rationale.

**Milestone**: Role approved by VP Merchandising.

### Step 3: Assess Current Performance

**Objective**: Understand where the category stands today.

Data to gather:
- **POS data**: Sales, units, velocity/store/week, margin % (manual pull — no MCP tool)
- **Market data**: Category size, growth rate, share by brand from SPINS/IRI (manual pull — no MCP tool)
- **Your performance vs market**: Are you growing faster or slower than the market?
- **Vendor data**: `mcp__sally-mcp__search_accounts` for vendor profiles within the category
- **Pipeline data**: `mcp__sally-mcp__search_opportunities` for pending vendor submissions in the category

**Deliverable**: Category performance assessment document with trends, gaps, and competitive position.

**Milestone**: Assessment reviewed by Category Analyst and Data Analyst.

### Step 4: Set the Scorecard

**Objective**: Define the KPIs that will measure category success.

Standard scorecard KPIs:

| KPI | Measurement | Frequency |
|-----|-------------|-----------|
| Category sales growth | % change vs prior year | Monthly |
| Velocity/store/week | $ and units per store per week | Weekly |
| Gross margin % | (Revenue - COGS) / Revenue | Monthly |
| ACV distribution | % of stores carrying the category | Quarterly |
| Out-of-stock rate | % of authorized SKUs not scanning | Weekly |
| New item success rate | % of new items exceeding velocity threshold at 90 days | Quarterly |
| Promotional lift | Incremental units during promo vs baseline | Per event |

**Deliverable**: Category scorecard with targets for each KPI.

**Milestone**: Scorecard approved by Director of Category Management.

### Step 5: Develop Strategy

**Objective**: Set the strategic direction for the category based on its role and performance assessment.

Strategy options (select based on category role):

| Strategy | When to Use | Actions |
|----------|------------|---------|
| Traffic builder | Destination categories needing more foot traffic | Competitive pricing, variety expansion, prominent placement |
| Transaction builder | Categories where basket size can grow | Cross-merchandising, trade-up assortment, bundle promotions |
| Cash generator | Mature categories with strong margins | Margin optimization, selective assortment, efficient promotions |
| Image enhancer | Categories that define the store's identity | Premium assortment, curation, storytelling, sampling |

**Deliverable**: Category strategy document with 3-5 strategic priorities.

**Milestone**: Strategy approved by VP Merchandising.

### Step 6: Select Tactics

**Objective**: Translate strategy into specific actions.

Tactical areas:
- **Assortment**: Add, remove, or adjust SKUs. New item approvals. Vendor changes.
- **Pricing**: Retail price adjustments. Competitive repositioning.
- **Promotions**: TPR schedule, endcap features, circular placements. Coordinated with `promo-calendar-manager` skill.
- **Shelf placement**: Planogram changes, facing adjustments, section relocation.
- **Vendor management**: Scorecard adjustments, vendor tier changes, new vendor onboarding.

**Deliverable**: Tactical plan with specific actions, owners, and timelines.

**Milestone**: Tactical plan reviewed by relevant team leads.

### Step 7: Implement

**Objective**: Execute the tactical plan.

Implementation checklist:
- [ ] Assortment changes communicated to vendors (adds, cuts, facing changes)
- [ ] New items onboarded through vendor compliance process
- [ ] Pricing changes entered in POS systems
- [ ] Planogram resets scheduled and communicated to store operations
- [ ] Promotional calendar updated with new promo events
- [ ] Vendor scorecards updated with new expectations
- [ ] Category team briefed on strategy and tactical changes

**Milestone**: Implementation complete — all tactics executed.

### Step 8: Review Results

**Objective**: Measure the impact of changes against the scorecard.

Timeline: Review at 30, 60, and 90 days post-implementation.

1. Pull updated POS data for all scorecard KPIs.
2. Compare vs pre-review baseline and vs targets.
3. Identify what worked and what did not.
4. Adjust tactics based on results (iterate, do not wait for next review cycle).
5. Document learnings for the next category review.

**Deliverable**: Post-implementation review document with results, learnings, and adjustments.

**Milestone**: Review presented to VP Merchandising.

## Limitations

- **Heavy manual data dependency**: Steps 3, 4, and 8 require POS and syndicated market data that are not available via MCP tools. Data must be pulled manually from retail systems or syndicated data providers.
- **No milestone tracking in MCP**: Milestone status must be tracked manually or in project management tools. No MCP tool for workflow state management.
- **No planogram integration**: Step 7 references planogram resets, but planogram tools (JDA, Blue Yonder) are outside Satellite's scope.
- **Vendor communication manual**: Notifications to vendors about assortment changes, scorecard updates, and new expectations must be sent manually.
