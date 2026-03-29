# Distributor Co

Agent Companies package for a national CPG distributor — models how a company like UNFI runs its operations through AI agents connected to Satellite's MCP tools. Covers supply chain, supplier management, catalog integrity, retail fulfillment, and analytics.

Built for [Paperclip](https://paperclipai.com) using the [Agent Companies](https://github.com/anthropics/agent-companies) protocol.

## Quick Start

```bash
npx paperclipai company import ./company/
```

## Org Chart

```
VP Operations (CEO equivalent)
├── Director of Supply Chain
│   ├── DC Operations Manager (warehouse ops, inventory, fill rates)
│   ├── Inventory Planner (reorder points, safety stock, demand forecasting)
│   └── Logistics Coordinator (shipping, routing, carrier management)
├── Director of Supplier Relations
│   ├── Supplier Onboarding Manager (application → evaluation → go-live)
│   ├── Supplier Scorecard Analyst (fill rate, OTIF, shelf-life, quality)
│   └── Category Manager (product selection, assortment planning)
├── Director of Catalog & Pricing
│   ├── Item Data Manager (product catalog, GS1, UPC/GTIN)
│   └── Pricing Analyst (cost tiers, billbacks, TPR validation)
├── VP Sales / Commercial
│   └── Retail Account Manager (retailer relationships, order management)
└── Data Analyst (cross-functional)
```

## Operating Principles

| Principle | What It Means |
|---|---|
| **Supply Chain Excellence** | Fill rates above 97%. Inventory allocation driven by demand signals and velocity thresholds. 55 DCs managed as a coordinated network. |
| **Supplier Portfolio Management** | Stage-gate onboarding. Monthly scorecards on fill rate, OTIF, shelf-life, quality. 10K+ suppliers evaluated and tiered. |
| **Catalog Integrity** | GS1-compliant product data. Controlled change process. Millions of SKUs maintained with validation at every step. |
| **Retail Fulfillment** | EDI-driven order processing. On-time delivery tracked by account. Substitutions and out-of-stocks managed at the line level. |
| **Data-Driven Operations** | Every KPI has an owner, a target, and a review cadence. Cross-functional reporting surfaces issues before they become crises. |

## Package Contents

| Type | Count |
|---|---|
| Company | 1 |
| Teams | 5 |
| Agents | 15 |
| Projects | 4 |
| Tasks | 7 |
| Skills | 4 |

## Model Strategy

| Tier | Model | Agents | Use Case |
|---|---|---|---|
| Frontier | Claude Opus | VP Operations | Strategic coordination, cross-functional decisions, weekly operations review |
| Standard | Claude Sonnet | Director of Supply Chain, Director of Supplier Relations, Director of Catalog & Pricing, VP Sales/Commercial | Functional leadership, team coordination, initiative ownership |
| Standard | Claude Sonnet | DC Operations Manager, Inventory Planner, Logistics Coordinator | Warehouse ops, demand forecasting, shipping coordination |
| Standard | Claude Sonnet | Supplier Onboarding Manager, Supplier Scorecard Analyst, Category Manager | Supplier lifecycle, scorecards, assortment planning |
| Standard | Claude Sonnet | Item Data Manager, Pricing Analyst | Product catalog maintenance, pricing management |
| Standard | Claude Sonnet | Retail Account Manager, Data Analyst | Retail relationships, cross-functional analytics |

## Skills

| Skill | Description |
|---|---|
| `supplier-onboarding-tracker` | Stage-gate workflow from application through go-live with compliance checklist. |
| `dc-stocking-matrix` | Product-by-DC allocation view with velocity thresholds and gap identification. |
| `supplier-scorecard-generator` | Structured scorecard template with fill rate, OTIF, shelf-life, and quality KPIs. |
| `catalog-update-processor` | Batch product update workflow with GS1 validation rules and change tracking. |

## Recurring Tasks

| Task | Assignee | Schedule |
|---|---|---|
| Daily Inventory Check | DC Operations Manager | Daily 7:00 AM CT |
| Daily Order Review | Retail Account Manager | Daily 8:00 AM CT |
| Weekly Fill Rate Review | DC Operations Manager | Monday 9:00 AM CT |
| Weekly Supplier Onboarding Status | Supplier Onboarding Manager | Tuesday 10:00 AM CT |
| Weekly Catalog Updates | Item Data Manager | Wednesday 9:00 AM CT |
| Monthly Supplier Scorecard | Supplier Scorecard Analyst | Monthly 1st |
| Monthly Pricing Review | Pricing Analyst | Monthly 5th |

## Protocol

This package follows the [Agent Companies v1](https://github.com/anthropics/agent-companies) specification. All agent files use YAML frontmatter with `name`, `title`, `description`, `slug`, `reportsTo`, and `skills`. The company structure is importable via the Paperclip CLI.

## License

MIT
