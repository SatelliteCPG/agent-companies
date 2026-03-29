# Partner Co

Agent Companies package for a CPG broker/partner — models how a company like Greenseed runs its multi-brand sales operation through AI agents connected to Satellite's MCP tools. Covers sales, client services, operations, and analytics across 50-100 brand principals.

Built for [Paperclip](https://paperclipai.com) using the [Agent Companies](https://github.com/anthropics/agent-companies) protocol.

## Quick Start

```bash
npx paperclipai company import ./company/
```

## Org Chart

```
Managing Partner (CEO equivalent)
├── VP Sales
│   ├── Territory Manager (territory-level pipeline ownership)
│   ├── Broker Sales Rep (the core field role — buyer meetings, sell-in)
│   └── Void Specialist (authorized-but-not-stocked gap closure)
├── VP Client Services
│   ├── Brand Onboarding Manager (new brand client intake)
│   └── Brand Performance Analyst (monthly reporting to brand principals)
├── Director of Operations
│   ├── Deduction Recovery Specialist (dispute invalid retailer deductions)
│   └── Category Review Coordinator (cross-brand review submissions)
└── Data Analyst (cross-functional analytics and dashboards)
```

## Operating Principles

| Principle | What It Means |
|---|---|
| **Multi-Brand Pipeline** | Pipeline tracked by brand and retailer. Aggregated views across 50-100 brands. No single-brand tunnel vision. |
| **Buyer Meeting Prep** | One meeting covers 3-10 brands. Sell sheets, pricing, promos, and distribution aggregated per retailer. |
| **Void Closure** | Authorized items not reaching shelves are tracked and closed. DC stocking vs authorization compared weekly. |
| **Deduction Recovery** | Invalid retailer deductions disputed on behalf of brand clients. Amounts, deadlines, and resolution tracked. |
| **Brand Reporting** | Monthly performance reports delivered to each brand principal — pipeline, placements, promos, deductions. |

## Package Contents

| Type | Count |
|---|---|
| Company | 1 |
| Teams | 5 |
| Agents | 12 |
| Projects | 4 |
| Tasks | 6 |
| Skills | 5 |

## Model Strategy

| Tier | Model | Agents | Use Case |
|---|---|---|---|
| Frontier | Claude Opus | Managing Partner | Strategic planning, brand portfolio decisions, cross-functional coordination |
| Standard | Claude Sonnet | VP Sales, VP Client Services, Director of Operations | Functional leadership, team coordination |
| Standard | Claude Sonnet | Territory Manager, Broker Sales Rep, Void Specialist | Field sales, pipeline ops, void closure |
| Standard | Claude Sonnet | Brand Onboarding Manager, Brand Performance Analyst | Brand client intake, monthly reporting |
| Standard | Claude Sonnet | Deduction Recovery Specialist, Category Review Coordinator | Deduction disputes, review submissions |
| Standard | Claude Sonnet | Data Analyst | Cross-brand dashboards, analytics |

## Skills

| Skill | Description |
|---|---|
| `multi-brand-meeting-brief` | Aggregate sell sheets and pipeline across N brands for one retailer meeting. |
| `partner-pipeline-dashboard` | Cross-brand pipeline view grouped by brand with rollup metrics. |
| `brand-performance-report` | Monthly summary per brand principal with pipeline and activity metrics. |
| `void-closure-report` | Compare authorized items against distributor DC stocking to surface gaps. |
| `brand-evaluation-scorecard` | Structured intake for evaluating whether to take on a new brand. |

## Recurring Tasks

| Task | Assignee | Schedule |
|---|---|---|
| Daily Email Triage | Broker Sales Rep | Daily 8:00 AM CT |
| Daily Pipeline Check | Territory Manager | Daily 9:00 AM CT |
| Weekly Buyer Meeting Prep | Broker Sales Rep | Monday 8:00 AM CT |
| Weekly Void Status Check | Void Specialist | Monday 10:00 AM CT |
| Weekly Brand Sync | Brand Performance Analyst | Friday 2:00 PM CT |
| Monthly Brand Performance Report | Brand Performance Analyst | 1st of month |

## Protocol

This package follows the [Agent Companies v1](https://github.com/anthropics/agent-companies) specification. All agent files use YAML frontmatter with `name`, `title`, `description`, `slug`, `reportsTo`, and `skills`. The company structure is importable via the Paperclip CLI.

## License

MIT
