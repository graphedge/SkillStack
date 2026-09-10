---
name: sumplan
description: >-
  Write a summary-proof handoff so the next session survives chat summarize.
  Use when the user sends /sumplan, sumplan, survive-summarize, or before ending
  a long multi-step feature session.
disable-model-invocation: true
---

# Sumplan — Summary-Proof Handoff

**Invoke:** `/sumplan [topic]` · `-ex @sumplan [topic]`

Derived from SkillStack `summary-proof-handoff` (Certified 2026-08-01). Target-repo alias; not SkillStack canon.

## When to write

Write a handoff when **any** of these are true:

- Session is long, context-heavy, or near summarize threshold (~75%).
- User sends `/sumplan`, sumplan, survive-summarize, or session recovery.
- Work spans files, gates, or smoke runs that future sessions must not re-discover.
- Decisions, evidence numbers, or "do not do X" locks must survive summarization.

**Do not** write for trivial one-file fixes unless the user asks.

## Output path

| Scope | Path |
|-------|------|
| Speckit feature (default) | `specs/<feature-id>/prompts/handoff-<feature>-<topic>.md` |
| Cross-feature / ops | `specs/prompts/handoff-<topic>.md` |

**Default feature**: the active speckit feature in the current repo (`<feature-id>`), unless `/sumplan` names another.

**Topic slug:** from `/sumplan` arg or infer from session (e.g. `phase14`, `next-gates`). Filename pattern: `handoff-<feature-id>-<topic>.md`.

Use **one primary handoff** per thread; link prior handoffs instead of duplicating.

## Workflow

1. **Parse invoke** — optional topic from `/sumplan <topic>`; default feature is the repo's active `<feature-id>`.
2. **Gather** from repo + session (not memory alone):
   - Worktree: the current repository root (do not hardcode a host path)
   - Branch and `git status` note
   - What passed / failed / partial (with numbers)
   - Spec locks and explicit deferrals
   - Single ordered next-action list (task IDs when applicable)
3. **Write** using [reference.md](reference.md) Feature Handoff template — fill every REQUIRED section; omit optional sections only when empty.
4. **Cross-link** spec, plan, tasks, prior handoffs, research appendices. Handoff = **index + recovery**, not a second spec.
5. **Platform note** when it blocks work: record the host/OS/shell gotcha that actually blocks the next step.
6. **Verify** with Session recovery checklist at bottom of template before finishing.

## Authoring rules

- **TL;DR first**: 5–7 numbered bullets; cold reader decides in ~30 seconds.
- **Preserve evidence**: test runs, row counts, exit codes, artifact paths — tables, not prose.
- **Locks vs open**: "must respect" table; "explicitly deferred" for out-of-scope.
- **Gate order**: dependency chain (`baseline PASS → code Txxx → re-smoke`).
- **Summarize recovery block** at top: next agent reads **this file first** + links to deep dives.
- **No secrets**: never paste `.env`, tokens, passwords.
- **Verbatim user locks**: quote or table exact rules — do not soften.

## Anti-patterns

| Avoid | Do instead |
|-------|------------|
| Re-explaining entire spec | Link spec + list deltas |
| "We discussed…" without artifacts | Paths, dates, numbers |
| Single wall of narrative | TL;DR + tables + gate order |
| Handoff per sub-task | One primary + linked satellites |
| Stale "DO NEXT" after work landed | Update status line + strike done items |

## Examples

See existing handoffs under `specs/<feature-id>/prompts/`. Template: [reference.md](reference.md).
