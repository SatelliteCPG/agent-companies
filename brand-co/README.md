# Brand Co

Agent Companies package for a CPG brand — models how a company like Just Egg runs its entire operation through AI agents connected to Satellite's MCP tools. Covers sales, marketing, distribution, finance, and analytics.

Built for [Paperclip](https://paperclipai.com) using the [Agent Companies](https://github.com/anthropics/agent-companies) protocol.

## Quick Start

```bash
npx paperclipai company import ./company/
```

## Org Chart

```
CEO (Brand Founder/GM)
├── VP Sales
│   ├── Sales Coordinator (daily CRM ops, email triage)
│   ├── Broker Manager (Greenseed, Acosta coordination)
│   └── Category Insights Analyst (SPINS data, competitive analysis)
├── VP Marketing
│   ├── Trade Marketing Manager (TPRs, MCBs, promotions)
│   └── Brand Manager (brand story, content, sellsheets)
├── VP Operations
│   ├── Distribution Manager (UNFI/KeHE DC coverage, codes)
│   └── Demand Planner (inventory, forecasting, fill rates)
└── VP Finance
    ├── Deduction Analyst (dispute, recover, reconcile)
    └── Data Analyst (P&L, scorecards, trade spend ROI)
```

## Operating Principles

| Principle | What It Means |
|---|---|
| **Sales Pipeline Management** | Every retailer interaction flows through a structured pipeline. Buyer meetings prepped with current data. Pipeline velocity tracked weekly. |
| **Distribution Coverage** | DC-level authorization tracked across UNFI, KeHE, and regionals. Distribution confirmed before sell-in effort. |
| **Trade Marketing** | Every promotion has planned cost and expected lift. Incremental volume measured vs baseline. Planned vs actual spend tracked by account. |
| **Financial Discipline** | P&L tracked by channel and retailer. Deductions disputed and recovered. Trade spend ROI measured on every dollar. |
| **Data-Driven Decisions** | SPINS, POS, distributor shipments, and CRM data drive all decisions. Category insights power sell-in stories. |

## Package Contents

| Type | Count |
|---|---|
| Company | 1 |
| Teams | 6 |
| Agents | 14 |
| Projects | 4 |
| Tasks | 8 |
| Skills | 5 |

## Model Strategy

| Tier | Model | Agents | Use Case |
|---|---|---|---|
| Frontier | Claude Opus | CEO | Strategic planning, cross-functional coordination, weekly business review |
| Standard | Claude Sonnet | VP Sales, VP Marketing, VP Operations, VP Finance | Functional leadership, team coordination, initiative ownership |
| Standard | Claude Sonnet | Sales Coordinator, Broker Manager, Category Insights Analyst | Daily CRM ops, broker coordination, SPINS analysis |
| Standard | Claude Sonnet | Trade Marketing Manager, Brand Manager | Promotion planning, brand content, sellsheets |
| Standard | Claude Sonnet | Distribution Manager, Demand Planner | DC coverage tracking, inventory forecasting |
| Standard | Claude Sonnet | Deduction Analyst, Data Analyst | Deduction recovery, P&L reporting, scorecards |

## Skills

| Skill | Description |
|---|---|
| `buyer-meeting-brief` | Prepare a buyer meeting brief with account history, SPINS data, distribution status, and talking points. |
| `pipeline-health-check` | Review pipeline velocity, stall points, and stage distribution across all active opportunities. |
| `account-deep-dive` | Pull full account profile — contacts, opportunities, distribution, promotions, and SPINS performance. |
| `email-triage` | Process inbound email threads into CRM records — contacts, meetings, opportunities, and tasks. |
| `distributor-status-report` | Report on DC-level authorization, fill rates, item codes, and onboarding status across distributors. |

## Recurring Tasks

| Task | Assignee | Schedule |
|---|---|---|
| Daily Email Triage | Sales Coordinator | Daily 8:00 AM CT |
| Daily Pipeline Check | Sales Coordinator | Daily 9:00 AM CT |
| Weekly Pipeline Review | VP Sales | Monday 10:00 AM CT |
| Weekly Distributor Status | Distribution Manager | Monday 11:00 AM CT |
| Weekly Trade Spend Review | VP Finance | Tuesday 9:00 AM CT |
| Weekly SPINS Analysis | Category Insights Analyst | Wednesday 9:00 AM CT |
| Weekly Deduction Aging Report | Deduction Analyst | Thursday 9:00 AM CT |
| Weekly Business Review | CEO | Friday 10:00 AM CT |

## Protocol

This package follows the [Agent Companies v1](https://github.com/anthropics/agent-companies) specification. All agent files use YAML frontmatter with `name`, `title`, `description`, `slug`, `reportsTo`, and `skills`. The company structure is importable via the Paperclip CLI.

## License

MIT
