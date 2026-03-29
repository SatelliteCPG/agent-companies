# Retailer Co

Agent Companies package for a CPG retailer — models how a company like Whole Foods runs its merchandising operation through AI agents connected to Satellite's MCP tools. Covers category management, vendor relations, merchandising, promotions, and analytics.

Built for [Paperclip](https://paperclipai.com) using the [Agent Companies](https://github.com/anthropics/agent-companies) protocol.

## Quick Start

```bash
npx paperclipai company import ./company/
```

## Org Chart

```
VP Merchandising
├── Director of Category Management
│   ├── Category Manager — Grocery
│   ├── Category Manager — Natural/Specialty
│   └── Category Analyst
├── Director of Vendor Relations
│   ├── New Item Evaluator
│   └── Vendor Compliance Manager
├── Director of Merchandising & Promotions
│   ├── Promotional Planner
│   └── Space Planning Analyst
└── Data Analyst (cross-functional)
```

## Operating Principles

| Principle | What It Means |
|---|---|
| **Category-First Decision Making** | Every assortment, vendor, and promo decision starts with category strategy. Category managers own P&L. |
| **Vendor Evaluation and Compliance** | Vendors earn shelf space through performance scorecards — fill rate, OTIF, quality, promo execution. |
| **Promotional Discipline** | Every promotion has planned cost and expected lift. Post-promo analysis measures incremental volume vs baseline. |
| **Data-Driven Assortment** | POS data, syndicated data, and vendor metrics drive assortment. Velocity and margin determine facings. |
| **Structured Review Cadence** | 8-step category management process. Reviews 1-2x/year per category. Weekly monitoring between reviews. |

## Package Contents

| Type | Count |
|---|---|
| Company | 1 |
| Teams | 5 |
| Agents | 11 |
| Projects | 4 |
| Tasks | 6 |
| Skills | 4 |

## Model Strategy

| Tier | Model | Agents | Use Case |
|---|---|---|---|
| Frontier | Claude Opus | VP Merchandising | Strategic planning, cross-functional coordination, category strategy |
| Standard | Claude Sonnet | Director of Category Management, Director of Vendor Relations, Director of Merchandising & Promotions | Functional leadership, team coordination, initiative ownership |
| Standard | Claude Sonnet | Category Manager — Grocery, Category Manager — Natural/Specialty, Category Analyst | Category P&L ownership, assortment, performance analysis |
| Standard | Claude Sonnet | New Item Evaluator, Vendor Compliance Manager | Submission scoring, vendor scorecards, compliance tracking |
| Standard | Claude Sonnet | Promotional Planner, Space Planning Analyst | Promo calendars, endcap allocation, planogram coordination |
| Standard | Claude Sonnet | Data Analyst | Cross-functional reporting, POS analysis, scorecards |

## Skills

| Skill | Description |
|---|---|
| `new-item-scorecard` | Structured evaluation rubric for vendor product submissions — margin, category fit, differentiation, supplier readiness. |
| `vendor-scorecard-review` | Pull vendor/supplier data and format into scorecard template with trend analysis. |
| `category-review-workflow` | Guided 8-step category management process with data templates and milestone tracking. |
| `promo-calendar-manager` | Track promotional events with timing, vendor funding, and performance measurement. |

## Recurring Tasks

| Task | Assignee | Schedule |
|---|---|---|
| Daily Sales Monitor | Category Analyst | Daily 8:00 AM CT |
| Weekly Vendor Scorecard Review | Vendor Compliance Manager | Monday 9:00 AM CT |
| Weekly New Item Review | New Item Evaluator | Tuesday 10:00 AM CT |
| Weekly Promo Calendar Check | Promotional Planner | Wednesday 9:00 AM CT |
| Monthly Category Performance Review | Category Manager — Grocery | 1st of month |
| Quarterly Category Review Kickoff | Director of Category Management | Quarterly |

## MCP Tool Coverage

Satellite's MCP server has 29 tools designed primarily for the brand/broker sell-in workflow. Retailer-co agents use available tools creatively where applicable (product catalog, account data, pipeline metrics) but many retailer-specific workflows require tools that do not yet exist. Each agent file is honest about gaps and describes what tools would be needed.

**Current coverage**: ~15-20% of retailer workflow needs.

## Protocol

This package follows the [Agent Companies v1](https://github.com/anthropics/agent-companies) specification. All agent files use YAML frontmatter with `name`, `title`, `description`, `slug`, `reportsTo`, and `skills`. The company structure is importable via the Paperclip CLI.

## License

MIT
