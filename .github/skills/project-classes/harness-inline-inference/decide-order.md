
# Decide-order: harness-manager work

**Invoke:** `-ex @harness-inline-inference/decide-order`

How Stack agents choose the **next hop** on a harness-manager repo (tmux-isolated inference **sources** with one-liner env recipes, plus on-demand **harness** windows that inherit that env). Not a charter for building developer-tool products.

## 1. Skill Signature

Given an ask about a harness manager or a candidate harness (a foreign agent product used as a client), choose the next hop without skipping desktop proof or Speckit.

## 2. Rationale

Agents with write access to a tool repo tend to implement stubs or open upstream PRs first. For a new harness slot or a foreign agent product, that invents glue before the one-liner contract is proven on a real machine.

**Do not skip desktop:** run the candidate harness on the desk against the relevant source one-liner **before** `implement_stub` or `upstream_contrib`, unless the operator explicitly ordered upstream work.

## 3. Input-Schema

```json
{
  "ask": "string",
  "target_harness_or_product": "string | null",
  "operator_authorized_repos": ["string"],
  "explicit_push_requested": "boolean"
}
```

## 4. Output-Schema

```json
{
  "next_hop": "explore_readonly | speckit_draft | desktop_trial | implement_stub | upstream_contrib | formation_note | stop_ask_operator",
  "why": "string",
  "must_not": ["string"]
}
```

## 5. Execution-Logic

1. If the ask needs a repo that is not operator-authorized → `stop_ask_operator`.
2. If the ask is “what is this / how does the one-liner work” and no Speckit Draft exists → prefer `explore_readonly` then `speckit_draft` (trials/strategy), not stubs.
3. If the ask is evaluate or integrate a new harness product → `desktop_trial` against the relevant source one-liner **before** `implement_stub` or `upstream_contrib`.
4. If the ask is formation/process (“how should agents decide”) → `formation_note` in the operator formation home (SkillStack / handoffs). **MUST NOT** default to adding `AGENTS.md` in the tool repo.
5. If `explicit_push_requested` is false → keep drafts local; state that in `why`.
6. Emit `must_not` including at least: multiline env paste; treating a **source** (the one-liner env) as a **harness** (the client window); upstream PR without desktop trials (unless the operator ordered it).

### Missing-hop gate

A name in an index is not a file. If a cited Speckit folder or skill path is absent, stop and ask — do not invent it.

### Constraints (class, not GTM)

- One-liner sources ≠ multiline paste. Source env files use one assignment per line; success UX announces one next step.
- Sources ≠ harnesses. The IDE/agent that supplies the env is a *source*; other agent products used as clients are *harnesses*.
- Speckit before stubs. Draft `specs/00N-…` before `harnesses/<name>.sh` or allowlist edits.
- Extra quota on one source may justify proving there first; it is sequencing, not the reason the one-liner exists.
