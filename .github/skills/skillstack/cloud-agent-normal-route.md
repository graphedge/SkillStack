---
name: cloud-agent-normal-route
description: >-
  Route cloud or harness agents on a parameterized implement / assess / sol
  loop. Use when launching or chaining agents on harness work — not Stratification
  Review Board lanes.
---
## [PUBLIC] Scope

Harness-runtime route for launching or chaining agents. **Not** a Board lane. Do not invent `debug` or `escalate-difficulty` lanes.

**Invoke:** `-ex @cloud-agent-normal-route <task-brief>`

Model names are **parameters**. This file does not make any vendor model snapshot law. Bind `implement_model`, `assess_model`, and `sol_model` in the launch prompt, or use the worked example below if you are on graphedge Grokbot.

## [PUBLIC] Route

1. **Preflight** — name scope, done-state, and success criteria. Put chunking in the launch prompt when the task is large.
2. **Implement** — launch `implement_model`. Never omit model.
3. **Assess / review** — launch `assess_model` when the task needs judgment, respecify, or review. Escalate only when needed, not by default.
4. **One bounce** — at most one implement↔assess retry.
5. **Logjam (`sol_model`)** — if still stuck, launch `sol_model`. It writes a **short packet** (what failed, what to change, what not to touch). Resume implement from that packet. This is harness standing, not a `workflow.md` heading.

## [PUBLIC] Worked example

Bind that works on **graphedge Grokbot** (example, not clone law):

- `implement_model` → `composer-2.5` (`fast: false`)
- `assess_model` → `grok-4.6` (`effort: medium`, `fast: false`)
- `sol_model` → `gpt-5.6-sol` (logjam solver after one bounce)

Never omit model. Prefer one coherent outcome per launch.

