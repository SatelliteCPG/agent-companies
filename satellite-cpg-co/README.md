# Satellite CPG

Agent Companies package for Satellite CPG — the platform that helps CPG brands manage CRM, products, communications, analytics, and content through human and AI interfaces.

Built for [Paperclip](https://paperclipai.com) using the [Agent Companies](https://github.com/anthropics/agent-companies) protocol.

## Quick Start

```bash
npx paperclipai company import ./company/
```

## Org Chart

```
CEO
├── CTO
│   ├── Backend Lead
│   │   ├── Backend Engineer (NestJS)
│   │   ├── Backend Engineer (Prisma)
│   │   └── Backend Engineer (ETL)
│   ├── Frontend Lead
│   │   ├── Frontend Engineer (Vue)
│   │   ├── Frontend Engineer (Mobile)
│   │   └── Frontend Engineer (Zapier)
│   ├── AI Lead
│   │   ├── AI Engineer (Sally)
│   │   └── AI Engineer (Scorecard)
│   └── DevOps Lead
│       ├── DevOps Engineer (CI/CD)
│       └── DevOps Engineer (Infra)
├── VP Product
│   ├── Product Manager (Platform)
│   └── Product Manager (AI)
├── VP Design
│   ├── Design Lead
│   │   ├── Designer (Web)
│   │   └── Designer (Mobile)
└── VP Engineering
    ├── QA Lead
    │   ├── QA Engineer (Backend)
    │   └── QA Engineer (Frontend)
    └── Security Lead
        └── Security Engineer
```

## The Compound Loop

Every feature ships through the compound engineering loop:

| Phase | Owner | What Happens |
|---|---|---|
| **Plan** | `/ce:plan` | Research agents examine repo patterns, prior solutions, and constraints. Produce structured plan with files, approach, risks. |
| **Work** | `/ce:work` | Execute plan with atomic commits. Git worktrees for parallel streams. Continuous verification after each step. |
| **Review** | `/ce:review` | Tiered persona reviewers (NestJS, Vue, Prisma, security, simplicity) run in parallel. Confidence-gated findings with autofix. |
| **Compound** | `/ce:compound` | $100 rule: if it saved future time, document it to `docs/solutions/` with YAML frontmatter. Next plan cycle finds it automatically. |

## Agent-Native Architecture

Four principles enforced by the `agent-native-architecture` reviewer on every PR:

1. **Parity** — Every UI action has an API equivalent. Sally can do anything a user can.
2. **Granularity** — One tool = one atomic operation. No wizard-locked flows.
3. **Composability** — Tools combine without side effects. Explicit inputs, no hidden state.
4. **Emergent Capability** — When the first three hold, agents discover workflows humans never designed.

## Package Contents

| Type | Count |
|---|---|
| Company | 1 |
| Teams | 7 |
| Agents | 21 |
| Projects | 4 |
| Tasks | 5 |
| Skills | 11 |
| References | 3 |

## Model Strategy

| Tier | Model | Use Case |
|---|---|---|
| Frontier | Claude Opus / Sonnet (latest) | Architecture decisions, complex planning, multi-file refactors |
| Standard | Claude Sonnet | Day-to-day implementation, code review, feature work |
| Volume | Claude Haiku | Linting, formatting, simple lookups, bulk operations |

## Skills

| Skill | Description |
|---|---|
| `ce-plan` | Transform feature descriptions into structured implementation plans grounded in repo patterns and research. |
| `ce-work` | Execute work plans efficiently with atomic commits and continuous verification. |
| `ce-review` | Structured code review using tiered persona agents with confidence-gated findings and autofix routing. |
| `ce-compound` | Document solved problems to compound team knowledge. Captures to `docs/solutions/` with YAML frontmatter. |
| `ce-brainstorm` | Explore requirements and approaches through collaborative dialogue before planning. |
| `agent-native-architecture` | Build applications where agents are first-class citizens. Audit parity, granularity, composability. |
| `impeccable-design` | Design vocabulary and quality enforcement. 20+ commands: critique, polish, audit, arrange, typeset, animate. |
| `satellite-issue` | End-to-end workflow for a GitHub issue — fetch, scope, plan, implement, verify, commit, PR. |
| `satellite-review` | Parallel multi-agent code review dispatching NestJS, Vue, Prisma, security, and simplicity reviewers. |
| `sally-tools` | Sally AI tool registry — 35 tools across 5 categories for CRM, Products, Communications, Analytics, Content. |
| `scorecard-skills` | Self-improving `.skill.json` data pipeline — AI maps once, deterministic code runs forever. |

## Recurring Tasks

| Task | Assignee | Schedule |
|---|---|---|
| Dependency audit | DevOps Engineer (CI/CD) | Weekly (Monday) |
| Security scan | Security Engineer | Weekly (Wednesday) |
| Performance regression check | QA Lead | Bi-weekly (Sprint start) |
| Prisma schema drift detection | Backend Engineer (Prisma) | Daily |
| Solution docs review | CTO | Monthly (1st) |

## Protocol

This package follows the [Agent Companies v1](https://github.com/anthropics/agent-companies) specification. All skill files use YAML frontmatter with `name`, `description`, `slug`, `tags`, and optional `metadata.sources`. Reference documents are freeform markdown. The company structure is importable via the Paperclip CLI.

## License

MIT
