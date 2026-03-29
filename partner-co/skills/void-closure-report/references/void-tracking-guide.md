# Void Tracking Guide

Operational guide for identifying, tracking, and closing distribution voids across a multi-brand broker portfolio.

## What is a Void?

A void occurs when a product is authorized to be on shelf at a retailer but is not actually available for purchase. The gap can occur at multiple points:

1. **DC Authorization Gap**: Product authorized by buyer but not yet set up at the serving distribution center
2. **DC Stocking Gap**: Product authorized at DC but not ordered or not in stock
3. **Store Ordering Gap**: DC has product but individual stores have not ordered it
4. **Shelf Placement Gap**: Product in store backroom but not placed on shelf

Satellite CRM currently tracks gaps at the DC level (types 1 and 2). Store-level tracking (types 3 and 4) requires retailer portal data not yet integrated.

## Void Identification Process

### Step 1: Establish the Authorization Baseline

For each closed-won opportunity in the CRM:
- Which product was authorized?
- At which retailer?
- Which DCs serve that retailer?
- When was the authorization granted?

### Step 2: Verify DC Setup

For each product-DC combination:
- Is there an active distributor code? (Check via `get_distributor_codes`)
- Is the product family authorized at the DC? (Check via `get_distributor_families`)
- Is there evidence of recent movement/orders?

### Step 3: Classify the Void

| Void Type | Signal | Typical Cause | Resolution Owner |
|-----------|--------|---------------|------------------|
| Code not set up | No distributor code exists | Onboarding not initiated | Director of Operations |
| Code pending | Code exists but status is pending | Distributor processing delay | Director of Operations |
| Code active, no movement | Active code but no orders | Store ordering issue | Broker Sales Rep |
| Family not authorized | DC does not carry the product family | Missing family-level authorization | Director of Operations |

## Void Prioritization Matrix

Prioritize voids by two dimensions: revenue impact and ease of closure.

| | Easy to Close | Hard to Close |
|---|---|---|
| **High Revenue** | Priority 1 — Fix immediately | Priority 2 — Escalate to leadership |
| **Low Revenue** | Priority 3 — Batch and resolve weekly | Priority 4 — Track but don't rush |

### Revenue Impact Estimation

Estimate weekly revenue lost per void:
- Product retail price x estimated units/week at the retailer
- Use category velocity benchmarks if store-specific data is unavailable
- Factor in retailer size (Kroger void > small regional void)

### Ease of Closure

- **Easy**: Code exists, just needs activation or reorder trigger
- **Medium**: Code needs to be created, typical 2-4 week timeline
- **Hard**: Requires new DC authorization, new distributor relationship, or retailer operational change

## Void Closure Timeline Benchmarks

| Resolution Type | Expected Timeline |
|----------------|-------------------|
| Code reactivation | 1-3 business days |
| New code setup at existing DC | 2-4 weeks |
| New DC authorization | 4-8 weeks |
| Store reorder trigger | 1-2 weeks |

## Multi-Brand Void Management

As a broker managing 50-100 brands:

1. **Batch by distributor**: When contacting UNFI about one brand's void, check all brands for voids at that same DC. One call, multiple resolutions.
2. **Batch by retailer**: When discussing voids with a buyer, cover all brands at once.
3. **Prioritize by brand profitability**: Brands with higher commission rates get faster void closure attention.
4. **Report by brand**: Each brand principal should see their own void metrics in the monthly performance report.

## Weekly Void Review Cadence

Every Monday at 10:00 AM CT:
1. Pull updated void list
2. Update closure status on previously identified voids
3. Identify new voids from authorizations won in the prior week
4. Assign closure actions to responsible parties
5. Report summary to VP Sales

## Escalation Rules

- Void open 30+ days with no progress: Escalate to VP Sales
- Void open 60+ days: Escalate to Managing Partner
- Multiple voids at the same DC: Investigate systemic issue with distributor
- Brand with 50%+ void rate: Flag to VP Client Services for brand principal communication
