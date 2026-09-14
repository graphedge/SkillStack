## [PUBLIC] Scope

The Board performs mandatory stratification review on skill and architecture proposals. Members are skill manifests, not runtime agents. Sequence: Strategy Lead → Pivot Lead → Skeptic.

## [PUBLIC] Placement

Add skills here when they define **governance personas**, veto rules, or the review workflow itself. Tactical utilities and domain logic belong in `core-operations/` or `project-classes/`.

## [PUBLIC] Constraints

- **Fast path (MUST):** Local tweak (one file, no new skill, no DNA change) MUST skip this Board sequence. See [workflow.md](workflow.md).
- **Change proposal (MUST):** Bounded suggestions use Change proposal in [workflow.md](workflow.md). Output a paste for an agent on the private operator source (SkillStack2). MUST NOT open a pull request or edit this snapshot directly. Unnamed lanes are locked.
- Architecture proposals MUST pass all three stages before implementation unless explicitly terminated.
- Each Board stage MUST write a named artifact (`strategy-record`, `pivot-record`, or `veto-record`). Personas are manifests, not runtime agents. Roleplay without an artifact does not count.
- Skeptic MAY VETO; a veto-record terminates the proposal.
- Operational requests MUST NOT amend Board DNA without `-mod`.

## [PUBLIC] Children

| Skill | Purpose |
|-------|---------|
| [strategy-lead.md](strategy-lead.md) | North Star alignment (stage 1) |
| [pivot-lead.md](pivot-lead.md) | Leverage and efficiency (stage 2) |
| [skeptic.md](skeptic.md) | Necessity, placement, depth (stage 3) |
| [workflow.md](workflow.md) | Fast path, Change proposal, Review sequence, lane lock |
| [clarifications.md](clarifications.md), [veto-guidelines.md](veto-guidelines.md) | Supporting governance |
| [governance/alignment-verification.md](governance/alignment-verification.md) | NON-CANON customer fill-in |
| [governance/necessity-audit.md](governance/necessity-audit.md) | NON-CANON customer fill-in |

## [PUBLIC] References

- Parent: [skill tree README](../README.md)
- Operator loop: [../core-operations/stratification-protocol.md](../core-operations/stratification-protocol.md)
- Runtime authority is the snapshot root README. The constitution is not in this snapshot.

