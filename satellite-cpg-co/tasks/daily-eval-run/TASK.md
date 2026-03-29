---
name: Daily Eval Run
description: Automated daily Promptfoo eval run with gating on tool-routing accuracy and regression pass rate.
slug: daily-eval-run
assignee: eval-engineer
project: compound-loop
schedule:
  timezone: America/Chicago
  startsAt: "2026-03-28T06:00:00-05:00"
  recurrence: daily
---

# Daily Eval Run

1. Build NestJS (cd app/api && npm run build).
2. Run Promptfoo (cd app/api/evals && ./run.sh).
3. Gate: tool-routing >=95%, regression = 100%.
4. Pass → log results.
5. Fail → create urgent task for sally-engineer + add to regression.yaml.
