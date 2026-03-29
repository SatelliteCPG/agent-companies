# Compound Loop Runbook

The Plan-Work-Review-Compound cycle for Satellite CPG engineering.

## The Loop

```
Plan → Work → Review → Compound
  ↑                        |
  └────────────────────────┘
```

Each cycle produces shipping code AND permanent knowledge.

## Phase 1: Plan

**Command:** `/ce:plan`

1. Agent reads the issue or feature description
2. Research agents fan out to examine repo patterns, existing modules, and prior solutions in `docs/solutions/`
3. Produces a structured plan: files to touch, approach, risks, verification criteria
4. Human reviews plan before execution

**Satellite specifics:**
- Backend plans reference NestJS module structure (70+ modules)
- Frontend plans reference Vue 3 component patterns
- Mobile plans reference Expo/React Native conventions
- Plans check Prisma schema for model impacts

## Phase 2: Work

**Command:** `/ce:work`

1. Agent executes plan step-by-step with atomic commits
2. Each commit is a single logical change
3. Git worktrees isolate parallel work streams
4. Continuous verification: tests run after each step

**Satellite specifics:**
- Backend: `pnpm test` for NestJS specs
- Frontend: `pnpm lint` + type-check
- Prisma migrations generated and tested
- Multi-tenant `orgId` enforcement verified on new endpoints

## Phase 3: Review

**Command:** `/ce:review`

Dispatches tiered persona reviewers in parallel:

| Reviewer | Focus |
|---|---|
| CE Reviewer | Compound engineering patterns, plan adherence |
| NestJS Reviewer | Module structure, guards, decorators, DI |
| Vue Reviewer | Composition API, Pinia stores, Ant Design Vue |
| Prisma Reviewer | Schema design, migrations, query efficiency |
| Security Reviewer | Auth, multi-tenancy, input validation |
| Simplicity Reviewer | Unnecessary complexity, over-engineering |

Findings are confidence-gated:
- **High confidence (>0.8):** Auto-fix and commit
- **Medium confidence (0.5-0.8):** Suggest fix, human approves
- **Low confidence (<0.5):** Flag for discussion

## Phase 4: Compound

**Command:** `/ce:compound`

The $100 rule: if solving this problem saved the team $100+ in future time, document it.

Creates a solution file in `docs/solutions/` with this format:

```yaml
---
module: crm
problem_type: data-migration
symptoms:
  - Contact import fails silently on duplicate emails
  - No error returned to API caller
root_cause: Prisma upsert swallows unique constraint violations when used with skipDuplicates
solution: Use createMany with explicit duplicate check and return rejected rows
prevention: Add integration test for duplicate handling on all bulk endpoints
tags:
  - prisma
  - bulk-operations
  - error-handling
---

## Context

[Narrative description of the problem and investigation]

## Solution

[Code snippets and explanation]

## Verification

[How to confirm the fix works]
```

## Iteration

After compounding, the next `/ce:plan` cycle benefits from the new solution doc. Research agents find it automatically. Knowledge compounds.
