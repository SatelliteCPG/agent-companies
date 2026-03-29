---
name: pipeline-health-check
description: "Analyze the sales pipeline for stale opportunities, missing follow-ups, and distribution gaps. Use during weekly pipeline reviews or when preparing for leadership updates."
slug: pipeline-health-check
tags:
  - sales
  - pipeline
  - analytics
  - weekly
---

# Pipeline Health Check

Analyze the full sales pipeline to surface stale opportunities, missing follow-ups, coverage gaps, and overall pipeline health. Designed for weekly pipeline review cadence.

## When to Use

- Weekly pipeline review (typically Monday morning)
- Preparing for a leadership or team status update
- User asks "what needs attention this week" or "show me pipeline health"
- Before quarterly business reviews to assess pipeline readiness

## Workflow

### Step 1: Pull Aggregate Pipeline Metrics

Call `mcp__sally-mcp__get_pipeline_metrics` to get the high-level pipeline snapshot:
- Total pipeline value
- Opportunity count by stage
- Average deal size
- Pipeline velocity indicators

Present the top-line numbers first so the user has context before diving into details.

### Step 2: Pull All Active Opportunities

Call `mcp__sally-mcp__search_opportunities` to retrieve all open/active opportunities. For each opportunity, note:
- Current stage
- Days in current stage
- Last activity date
- Expected close date
- Associated account and contacts

### Step 3: Identify Stalled Opportunities

Apply the stall thresholds from `references/pipeline-review-framework.md`:

| Stage | Expected Duration | Stall Threshold |
|-------|------------------|-----------------|
| Prospecting | 1-2 weeks | 21 days |
| Qualification | 2-4 weeks | 30 days |
| Proposal | 2-4 weeks | 30 days |
| Negotiation | 1-3 weeks | 21 days |
| Category Review | Varies by retailer | 60 days (unless known review window) |

Flag any opportunity exceeding its stall threshold. Sort flagged opportunities by value (highest first).

### Step 4: Check Account Coverage

Call `mcp__sally-mcp__search_accounts` to get the full account list. Cross-reference against opportunities:

- **Accounts with no open opportunities** — potential gap in coverage
- **Accounts with no meeting in 30+ days** — check via `mcp__sally-mcp__list_meetings`
- **Accounts with multiple stalled opportunities** — may indicate relationship issues

### Step 5: Check Upcoming Activities

Call `mcp__sally-mcp__get_upcoming` to see scheduled meetings and follow-ups:

- Are there meetings scheduled for this week?
- Are any high-priority opportunities missing a next meeting?
- Are there any overdue follow-ups?

### Step 6: Compile the Pipeline Report

```
# Pipeline Health Check — Week of [date]

## Summary Metrics
- Total pipeline value: $[X]
- Active opportunities: [N]
- Opportunities by stage: [breakdown]
- Deals closing this month: [N] worth $[X]

## Attention Required (sorted by urgency)

### Stalled Opportunities
| Opportunity | Account | Stage | Days Stalled | Value | Recommended Action |
|-------------|---------|-------|-------------|-------|--------------------|
| ...         | ...     | ...   | ...         | ...   | ...                |

### Accounts Without Recent Activity
| Account | Last Meeting | Open Opportunities | Recommended Action |
|---------|-------------|-------------------|-------------------|
| ...     | ...         | ...               | ...               |

### Upcoming This Week
| Date | Meeting/Activity | Account | Related Opportunity |
|------|-----------------|---------|-------------------|
| ...  | ...             | ...     | ...               |

## Pipeline Velocity
- Average days to close (last 90 days): [X]
- Win rate (last 90 days): [X]%
- Deals advanced this week: [N]
- Deals lost this week: [N]

## Recommended Priorities This Week
1. [Highest-value stalled deal — specific next action]
2. [Account needing re-engagement — specific outreach suggestion]
3. [Opportunity approaching close date — what's needed to close]
4. [New opportunity to create — account gap identified]
5. [Meeting to schedule — account without recent touchpoint]
```

### Step 7: Generate Action Items

For each flagged item, generate a specific, actionable recommendation:

- **Stalled deal**: "Schedule a check-in call with [buyer] at [account] — last contact was [date]. Suggested topic: [based on opportunity stage]."
- **Account gap**: "No open opportunities at [account]. Last meeting was [date]. Consider reaching out about [product family not yet pitched]."
- **Missing meeting**: "[Opportunity] at [account] has no scheduled next step. Recommend scheduling [type of meeting] by [date]."

## Configuration

The user can customize stall thresholds by updating `references/pipeline-review-framework.md`. Default thresholds are intentionally conservative for CPG sales cycles (longer than SaaS).

## Limitations

- **Opportunity aging**: If `search_opportunities` does not return a `last_activity_date` or `days_in_stage` field, this skill estimates from available timestamps. Accuracy depends on CRM data completeness.
- **Win/loss rates**: Require historical closed opportunities. If the CRM is new, these metrics will be unreliable.
- **Competitive context**: Not available from CRM data alone. SPINS integration would enhance gap identification.
