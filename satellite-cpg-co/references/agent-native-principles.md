# Agent-Native Architecture Principles

Satellite CPG builds agent-native applications where AI agents are first-class citizens, not afterthoughts bolted onto human-only interfaces.

## The Four Principles

### 1. Parity

Every action a human can take in the UI must be available to an agent via API.

- Sally can do everything a dashboard user can do
- No "admin-only" features hidden behind UI-only flows
- Tool registry mirrors UI capabilities 1:1

**Satellite example:** Sally's 35 tools cover every CRM, product, communications, analytics, and content operation available in the web app.

### 2. Granularity

Expose atomic operations, not monolithic workflows.

- One tool = one action
- Agents compose tools; humans compose clicks
- Never force an agent through a multi-step wizard

**Satellite example:** `createContact` and `addContactTag` are separate tools. An agent composes them; the UI bundles them into a form.

### 3. Composability

Tools combine without side effects or hidden coupling.

- Stateless where possible
- Explicit inputs and outputs
- No implicit ordering dependencies

**Satellite example:** Sally tools accept `orgId` explicitly on every call. No hidden session state.

### 4. Emergent Capability

When parity + granularity + composability hold, agents discover workflows humans never designed.

- Agents chain tools in novel sequences
- New use cases emerge without new code
- The tool surface area becomes a platform

**Satellite example:** Sally autonomously sequences CRM lookups, product queries, and email drafts to handle broker inquiries end-to-end.

## Anti-Patterns

| Anti-Pattern | Symptom | Fix |
|---|---|---|
| UI-only action | Agent cannot perform operation | Add API endpoint + tool |
| Wizard-locked flow | Tool requires multi-step state | Decompose into atomic tools |
| Implicit context | Tool relies on session/cookie | Pass context explicitly |
| God tool | Single tool does everything | Split into composable units |
| Human-in-the-loop gate | Agent blocked waiting for approval on routine ops | Add confidence thresholds |
| Inconsistent naming | `getContact` vs `fetch_product` | Standardize verb + noun |

## Architecture Review Checklist

Use this checklist when reviewing any new module, endpoint, or feature:

- [ ] **Parity:** Can Sally perform this action via tool call?
- [ ] **Granularity:** Is this the smallest useful operation?
- [ ] **Composability:** Does this tool work without depending on prior tool calls?
- [ ] **Naming:** Does it follow `verbNoun` convention matching existing tools?
- [ ] **Auth:** Does it respect `orgId` multi-tenancy?
- [ ] **Idempotency:** Is the operation safe to retry?
- [ ] **Error shape:** Does it return structured errors an agent can parse?
- [ ] **Documentation:** Is the tool registered in Sally's tool registry with description and schema?
