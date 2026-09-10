## [PUBLIC] Scope

Verify skills enforce architectural compliance. This snapshot ships NON-CANON customer fill-ins under `core/` and `governance/`, not a full audit runtime.

## [PUBLIC] Placement

Add skills here for **audits and pre-implementation checks**. Product features and domain flows belong elsewhere. Board veto logic stays in `board/`.

## [PUBLIC] Constraints

- Findings MUST be actionable (pass/fail criteria, not subjective essays).
- Audits MUST NOT mutate files during `-ex` runs.
- Files in this folder that are customer fill-ins are NON-CANON. MUST NOT treat them as law.
- Fast-path tweaks MUST NOT run a verify suite.

## [PUBLIC] Children

| Path | Role |
|------|------|
| [core/complexity-audit.md](core/complexity-audit.md) | NON-CANON customer fill-in |
| [core/dependency-enforcement.md](core/dependency-enforcement.md) | NON-CANON customer fill-in |
| [core/depth-check.md](core/depth-check.md) | NON-CANON customer fill-in |
| [core/path-audit.md](core/path-audit.md) | NON-CANON customer fill-in |
| [core/spec-linting-before-code.md](core/spec-linting-before-code.md) | NON-CANON customer fill-in |
| [core/statelessness-audit.md](core/statelessness-audit.md) | NON-CANON customer fill-in |
| [governance/benny-review.md](governance/benny-review.md) | NON-CANON customer fill-in |
| [governance/final-review.md](governance/final-review.md) | NON-CANON customer fill-in |

## [PUBLIC] References

- Parent: [skill tree README](../README.md)
- Runtime authority is the snapshot root README. The constitution is not in this snapshot.

