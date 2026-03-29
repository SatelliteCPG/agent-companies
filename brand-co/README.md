# Brand Co

Agent Companies package for a CPG brand sales team — models how a company like Just Egg uses Satellite to manage retail sell-in, distributor relationships, and broker coordination through Sally AI.

Built for [Paperclip](https://paperclipai.com) using the [Agent Companies](https://github.com/anthropics/agent-companies) protocol.

## Quick Start

```bash
npx paperclipai company import ./company/
```

## Org Chart

```
Sales Director
├── Sales Coordinator (Sally's brand-facing persona)
├── Trade Marketing Analyst
├── Distributor Liaison
└── Data Analyst
```

## The Compound Loop (Brand Sales)

Every week flows through the brand sales compound loop:

| Phase | Owner | What Happens |
|---|---|---|
| **Plan** | Sales Director | Review pipeline health, identify distribution gaps, prioritize retailers and broker follow-ups for the week. |
| **Execute** | Sales Coordinator | Triage emails to CRM, prepare buyer meeting briefs, process sample requests, update opportunity stages. |
| **Review** | Sales Director + Data Analyst | Weekly pipeline review, broker performance check, distributor authorization verification. |
| **Compound** | Sales Director | Capture what worked — which pitches landed, which retailers responded, which broker tactics moved deals. Feed into next week's plan. |

## MCP Tool Surface

The brand team relies on Sally's 35 MCP tools. Core tools by workflow:

| Workflow | Key MCP Tools |
|---|---|
| Email Triage | `process_email_thread`, `create_contact`, `create_meeting`, `create_opportunity`, `update_opportunity` |
| Buyer Meeting Prep | `search_accounts`, `get_company`, `search_contacts`, `search_opportunities`, `get_sellsheet`, `get_upcoming` |
| Pipeline Review | `get_pipeline_metrics`, `search_opportunities`, `list_account_families` |
| Distributor Check | `get_distributor_codes`, `get_distributor_families`, `list_distributors`, `search_distribution_centers` |
| Broker Coordination | `get_company`, `search_contacts`, `list_meetings`, `search_opportunities` |

## Package Contents

| Type | Count |
|---|---|
| Company | 1 |
| Teams | 2 |
| Agents | 5 |
| Projects | 2 |
| Tasks | 3 |
| Skills | 0 (shipped separately in Unit 5) |

## Model Strategy

| Tier | Model | Use Case |
|---|---|---|
| Frontier | Claude Opus | Sales Director — strategic pipeline decisions, weekly planning, broker accountability |
| Standard | Claude Sonnet | All other agents — email triage, meeting prep, data analysis, distributor checks |

## Recurring Tasks

| Task | Assignee | Schedule |
|---|---|---|
| Daily Email Triage | Sales Coordinator | Daily 8:00 AM CT |
| Daily Pipeline Check | Sales Coordinator | Daily 9:00 AM CT |
| Weekly Distributor Review | Distributor Liaison | Monday 10:00 AM CT |

## Protocol

This package follows the [Agent Companies v1](https://github.com/anthropics/agent-companies) specification. Skills are shipped as separate packages (see Unit 5 — brand-specific SKILL.md files). The company structure is importable via the Paperclip CLI.

## License

MIT
