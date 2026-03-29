---
name: Brand Co
description: CPG brand sales team using Satellite to manage retail sell-in pipeline, distributor relationships, and broker coordination. Reference company — Just Egg.
slug: brand-co
schema: agentcompanies/v1
version: 1.0.0
license: MIT
authors:
  - name: JD Fiscus
tags:
  - cpg
  - brand
  - sales
  - retail-sell-in
  - pipeline-management
metadata:
  sources:
    - kind: github-dir
      repo: iamfiscus/agent-companies
      path: brand-co
      commit: main
      url: https://github.com/iamfiscus/agent-companies/tree/main/brand-co
---

# Brand Co

Agent-company package for a CPG brand sales team running on Satellite. Models how a brand like Just Egg uses Sally and the Satellite MCP tool suite to manage its retail sales pipeline — from email triage through buyer meetings, pipeline reviews, and distribution gap analysis.

## Operating Principles

### Sales-First Architecture

- **Pipeline is truth:** Every retailer interaction flows through the opportunity pipeline. Email triage creates opportunities, buyer meetings advance them, pipeline reviews identify stalls.
- **CRM capture at the edge:** Emails, meetings, and broker reports are processed into structured CRM data as they arrive — not batched at end-of-week.
- **Distribution drives strategy:** Distributor authorization data (DCs, product families, codes) determines where sell-in effort is focused. No point pitching a retailer if the DC is not set up.
- **Broker accountability:** Broker partners are tracked through meetings held, opportunities advanced, and territory coverage gaps — not just relationship warmth.

### The Compound Loop (Brand Sales)

All work flows through four phases:

1. **Plan** — Review pipeline health, identify distribution gaps, prioritize retailers for the week. Use `get_pipeline_metrics`, `search_opportunities`, `list_account_families`.
2. **Execute** — Run email triage, prepare buyer meeting briefs, process sample requests, update opportunity stages. Use `process_email_thread`, `search_accounts`, `create_meeting`, `update_opportunity`.
3. **Review** — Weekly pipeline review, broker coordination check, distributor status verification. Use `pipeline-review` prompt, `get_distributor_families`, `list_meetings`.
4. **Compound** — Capture what worked: which talking points landed, which retailers responded to which pitch angles, which broker tactics moved deals. Feed learnings into next week's plan.

Learnings feed back into the next Plan cycle. This is how the sales team compounds institutional knowledge instead of losing it to turnover.

### Default Rules

- No buyer meeting happens without a meeting brief prepared via `buyer-meeting-prep`
- No email goes unprocessed — every inbound thread gets triaged through `email-to-crm-upsert`
- Pipeline review happens weekly without exception
- Distributor authorization is verified before any new sell-in push
- Broker performance is reviewed weekly with quantifiable metrics
- All opportunity stage changes require a note explaining why
