---
name: distributor-status-report
description: "Generate a distributor performance and coverage report. Use when reviewing distributor relationships, checking DC coverage, or preparing for distributor meetings."
slug: distributor-status-report
tags:
  - distribution
  - reporting
  - weekly
---

# Distributor Status Report

Generate a comprehensive distributor coverage report showing which DCs carry which products, gaps in coverage, and distributor code status. Designed for weekly distribution reviews and distributor meeting prep.

## When to Use

- Weekly distribution check-in
- Preparing for a distributor meeting (UNFI, KeHE, etc.)
- User asks about DC coverage, authorization status, or distribution gaps
- Before buyer meetings where distribution status is relevant
- When onboarding a new product and need to verify distributor setup

## Workflow

### Step 1: Identify Scope

Ask the user (if not already clear):
- All distributors or a specific one (e.g., UNFI, KeHE)?
- All products or a specific product family?
- All regions or a specific DC/region?

### Step 2: Pull Distributor Overview

1. Call `mcp__sally-mcp__list_distributors` to get the full distributor list with their metadata
2. For each distributor in scope, call `mcp__sally-mcp__get_distributor_codes` to verify code status (active, pending, inactive)
3. Note any codes that are pending setup or recently deactivated

### Step 3: Map DC Coverage

1. Call `mcp__sally-mcp__search_distribution_centers` to get all DCs for the distributors in scope
2. For each DC, call `mcp__sally-mcp__get_distributor_families` to see which product families are authorized at that DC
3. Call `mcp__sally-mcp__search_products` to get the full product catalog for cross-reference

Build a coverage matrix: Product Families (rows) x Distribution Centers (columns).

### Step 4: Identify Gaps

Analyze the coverage matrix for three types of gaps:

**Type A — Product not authorized at any DC in a region**
- A product family exists in the catalog but has zero DC authorizations in a geographic region
- Action: Initiate distributor authorization process

**Type B — DC carries some products but not all families**
- A DC is set up and active but missing one or more product families
- Action: Submit additional product authorization to the DC

**Type C — Distributor code issues**
- Active products mapped to pending or inactive distributor codes
- Action: Follow up with distributor on code activation

### Step 5: Compile the Report

```
# Distributor Status Report — [Date]

## Distributor Summary
| Distributor | Active Codes | Pending Codes | Total DCs | Product Families Covered |
|-------------|-------------|---------------|-----------|------------------------|
| UNFI        | [N]         | [N]           | [N]       | [N] of [total]         |
| KeHE        | [N]         | [N]           | [N]       | [N] of [total]         |

## Coverage Matrix

### UNFI Distribution Centers
| DC Location | Region | [Family 1] | [Family 2] | [Family 3] | ... |
|-------------|--------|------------|------------|------------|-----|
| Lancaster   | East   | ✓          | ✓          | ✗          | ... |
| Moreno Vly  | West   | ✓          | ✗          | ✗          | ... |
| ...         | ...    | ...        | ...        | ...        | ... |

### KeHE Distribution Centers
| DC Location | Region | [Family 1] | [Family 2] | [Family 3] | ... |
|-------------|--------|------------|------------|------------|-----|
| ...         | ...    | ...        | ...        | ...        | ... |

## Coverage Gaps

### Priority Gaps (blocks active opportunities)
| Gap Type | Product Family | DC / Region | Impact | Recommended Action |
|----------|---------------|-------------|--------|--------------------|
| A        | [family]      | [region]    | [desc] | Initiate auth      |
| B        | [family]      | [DC]        | [desc] | Submit to DC       |

### Code Issues
| Distributor | Code | Status  | Product Family | Action Needed |
|-------------|------|---------|---------------|---------------|
| ...         | ...  | Pending | ...           | Follow up     |

## Distribution Health Score
- Overall coverage: [X]% of product-DC combinations authorized
- Regions at full coverage: [list]
- Regions with gaps: [list]
```

### Step 6: Cross-Reference with Pipeline

For identified gaps, check whether there are active opportunities that depend on distribution at the gap location:

1. Call `mcp__sally-mcp__search_opportunities` to find opportunities at accounts served by the gap DC
2. Flag any opportunities where the gap could block a sale
3. Prioritize gap closure for these opportunities

## Notes

- The `distributor-check` MCP prompt provides a starting framework — invoke it if available, then supplement with the detailed tool calls above
- Distribution authorization timelines vary: UNFI typically 2-4 weeks, KeHE 1-3 weeks. Factor this into opportunity timelines.
- This report pairs well with `buyer-meeting-brief` — distribution status is a required section of every meeting brief
- For detailed distributor management context, see `references/distributor-management-guide.md`
