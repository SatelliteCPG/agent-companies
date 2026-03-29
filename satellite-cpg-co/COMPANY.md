---
name: Satellite CPG
description: Agent Native B2B SaaS for Consumer Packaged Goods. Humans love the UI/UX, machines love the agent-native architecture. Every sprint compounds.
slug: satellite-cpg
schema: agentcompanies/v1
version: 1.0.0
license: MIT
authors:
  - name: JD Fiscus
tags:
  - cpg
  - agent-native
  - compound-engineering
  - b2b-saas
metadata:
  sources:
    - kind: github-dir
      repo: iamfiscus/agent-companies
      path: satellite-cpg
      commit: main
      url: https://github.com/iamfiscus/agent-companies/tree/main/satellite-cpg
---

# Satellite CPG

Agent Native platform for CPG sales teams. NestJS API with 70+ modules, Vue 3 frontend, Expo mobile app, Sally AI chatbot with 35 tools, Just Scorecard data pipeline, and Zapier integration — orchestrated through the Compound Engineering loop.

## Operating Principles

### Agent-Native Architecture

- **Parity:** Whatever a user can do through the UI, an agent must be able to achieve through tools. Sally's 35 tools across 5 categories (CRM, Products, Communications, Analytics, Content) demonstrate this.
- **Granularity:** Prefer atomic primitives. Sally's email-processing agent composes 7 atomic tools into a full workflow — no workflow-shaped tools needed.
- **Composability:** New features ship as new prompts, not new code. Adding "log meeting notes from email" requires zero new tools.
- **Emergent Capability:** Agents handle unexpected queries by composing search + CRUD primitives.

### The Compound Loop

All work flows through four phases:

1. **Plan** — Research the codebase via `/ce:plan`, check institutional learnings in `docs/solutions/`, design the approach
2. **Work** — Execute with `/ce:work` or `/lfg`, atomic commits, git worktree isolation, Mission Control 3-lane setup
3. **Review** — Multi-agent audit via `/ce:review` across security, performance, architecture, and agent-native compliance
4. **Compound** — Capture learnings via `/ce:compound` so the next cycle is easier. $100 rule: every preventable failure gets a permanent fix.

Learnings feed back into the next Plan cycle. This is the company's core operating mechanism.

### Default Rules

- No task ships without review via `/ce:review`
- No bug is fixed without a compound doc via `/ce:compound`
- No plan is written without checking institutional learnings first
- Every feature must maintain agent-native parity
- All Sally tool changes must pass Promptfoo evals (>95% routing, 100% regression)
- All Prisma schema changes require CTO approval
- All auth/security changes require CTO + security review
- Frontend PRs trigger `impeccable:critique` + `impeccable:audit`
