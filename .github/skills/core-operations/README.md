## [PUBLIC] Scope

Core operations are cross-cutting horizontal skills reused across project classes. This snapshot ships writing canon, the operator loop, and NON-CANON customer fill-ins for mode and state slots.

## [PUBLIC] Placement

Add a skill here when **two or more project classes** would duplicate the same behavior. Domain-specific rules stay in `project-classes/`. Board personas stay in `board/`. Executable L3 flows stay in `skill-flows/`.

## [PUBLIC] Constraints

- Skills MUST be stateless; required state passes through inputs and outputs. The `state-management` file in this snapshot is a NON-CANON customer fill-in, not law.
- Apply `-ex` vs `-mod` from the skill-tree README. The `mode-selection` file in this snapshot is a NON-CANON customer fill-in, not law.
- Writing canon lives under `writing/`; management tooling under `management/`.
- If a named core-op file is not in this snapshot: this pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator.

## [PUBLIC] Children

| Subfolder / file | Role |
|------------------|------|
| [writing/](writing/README.md) | Documentation and harness standards |
| [management/](management/README.md) | Placement index (no management leaves here) |
| [stratification-protocol.md](stratification-protocol.md) | Operator loop (viability → Board → manifests) |
| [mode-selection.md](mode-selection.md) | NON-CANON customer fill-in |
| [state-management.md](state-management.md) | NON-CANON customer fill-in |
| `qa`, `dependency-syntax`, `reusability-validation` | This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. |

## [PUBLIC] References

- Parent: [skill tree README](../README.md)
- Runtime authority is the snapshot root README. The constitution is not in this snapshot.

