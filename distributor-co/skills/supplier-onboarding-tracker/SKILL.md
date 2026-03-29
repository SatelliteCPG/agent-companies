---
name: supplier-onboarding-tracker
description: "Track and manage a supplier through the 5-stage onboarding pipeline from application through go-live. Use when onboarding a new supplier, checking onboarding status, or reviewing the supplier pipeline."
slug: supplier-onboarding-tracker
tags:
  - suppliers
  - onboarding
  - pipeline
  - compliance
---

# Supplier Onboarding Tracker

Track and manage a supplier through the 5-stage onboarding pipeline — Application, Evaluation, Compliance, Setup, Go-Live. Designed for national distributors processing 100+ new supplier applications per month at scale.

## When to Use

- User asks to onboard a new supplier or brand
- User asks to check the status of a supplier in the onboarding pipeline
- User asks to review the onboarding pipeline (how many at each stage)
- User asks about compliance requirements for a new supplier
- User asks to move a supplier to the next onboarding stage

## Workflow

### Step 1: Identify the Supplier and Stage

Ask the user (if not already provided):
- Supplier/brand name and primary contact
- Which stage are they in (or is this a new application)?
- Any known blockers or issues

### Step 2: Set Up or Retrieve Supplier Record

For new suppliers:
1. Call `mcp__sally-mcp__create_company` with the supplier's company information
2. Call `mcp__sally-mcp__create_contact` for the primary supplier contact
3. Call `mcp__sally-mcp__create_account` to establish the supplier account record
4. Call `mcp__sally-mcp__create_opportunity` to create the onboarding pipeline entry — use stage to track pipeline position

For existing suppliers:
1. Call `mcp__sally-mcp__search_accounts` with the supplier name
2. Call `mcp__sally-mcp__search_opportunities` to find the onboarding opportunity
3. Call `mcp__sally-mcp__search_contacts` to retrieve supplier contacts

### Step 3: Evaluate Stage-Specific Requirements

Reference the stage requirements in `references/supplier-onboarding-stages.md` and check:

**Stage 1 — Application:**
- Company information complete (legal name, address, DUNS, tax ID)
- Product catalog submitted (product list, descriptions, pricing)
- Initial documentation received (insurance, food safety certification)

**Stage 2 — Evaluation:**
- Category fit assessment by Category Manager
- Margin analysis (supplier cost vs. distributor target margin)
- Market demand evidence (retailer requests, market data)
- Decision: proceed, hold, or decline
- No MCP tool for evaluation scoring yet — use the checklist in references/

**Stage 3 — Compliance:**
- GS1/GDSN registration verified — supplier has valid company prefix and GTINs
- EDI capability confirmed (850, 810, 856 support or portal-based alternative)
- Insurance documentation current (general liability, product liability, workers comp)
- Food safety certification valid (SQF, BRC, FSSC 22000, or equivalent)
- Labeling compliance verified (USDA/FDA requirements for the category)
- No MCP tool for compliance document tracking yet — this is managed via checklists

**Stage 4 — Setup:**
- Product data entered: Call `mcp__sally-mcp__search_products` to verify items exist; use `mcp__sally-mcp__get_product` to check data completeness
- Pricing configured: cost, list price, bracket pricing, promotional allowances
- DC allocation determined: Call `mcp__sally-mcp__search_distribution_centers` and `mcp__sally-mcp__get_distributor_codes` to verify DC setup
- EDI trading partner setup and test transactions completed
- Initial purchase order quantities calculated

**Stage 5 — Go-Live:**
- Initial PO placed and confirmed
- First shipment received and inspected at assigned DCs
- Distributor codes activated: verify via `mcp__sally-mcp__get_distributor_codes`
- Call `mcp__sally-mcp__update_opportunity` to mark onboarding as complete
- Supplier transitions to ongoing management (Supplier Scorecard Analyst)

### Step 4: Advance or Document Status

If the supplier is ready to advance:
1. Verify all requirements for the current stage are met
2. Call `mcp__sally-mcp__update_opportunity` to update the stage
3. Notify the next responsible party (e.g., Category Manager for Evaluation, Item Data Manager for Setup)

If there are blockers:
1. Document the specific blocker and required action
2. Identify the responsible party
3. Set a follow-up date
4. Log as activity note on the opportunity

### Step 5: Generate Status Report

```
# Supplier Onboarding Status: [Supplier Name]

**Stage**: [1-Application / 2-Evaluation / 3-Compliance / 4-Setup / 5-Go-Live]
**Application Date**: [date]
**Days in Pipeline**: [N]
**Days in Current Stage**: [N]

## Stage Checklist
- [x] Completed items
- [ ] Pending items
- [!] Blocked items — [blocker description]

## Key Contacts
| Role | Name | Email | Last Contact |
|------|------|-------|-------------|
| Primary | ... | ... | ... |
| Category Manager | ... | ... | ... |

## Products
| Product | GTIN | Category | Status |
|---------|------|----------|--------|
| ... | ... | ... | Pending setup / Active |

## DC Allocation
| DC | Region | Status |
|----|--------|--------|
| ... | ... | Pending / Active |

## Timeline
- Application received: [date]
- Evaluation complete: [date or pending]
- Compliance verified: [date or pending]
- Setup complete: [date or pending]
- Go-live: [date or projected]

## Blockers
| Blocker | Owner | Due Date | Status |
|---------|-------|----------|--------|
| ... | ... | ... | Open / Resolved |
```

## Notes

- The `email-to-crm-upsert` MCP prompt is useful for capturing supplier communications during onboarding — invoke it when processing supplier emails
- Average onboarding timeline: 60-120 days for new suppliers. Existing vendors adding SKUs: 2-4 weeks.
- GS1 registration can be the longest blocker — if the supplier doesn't have a company prefix, this alone can take 4-6 weeks
- For detailed stage requirements, see `references/supplier-onboarding-stages.md`
