## [PUBLIC] Scope

SkillStack skill canon root. Skills follow a three-level model: Level 1 (Board / strategic), Level 2 (project classes and core operations), Level 3 (skill flows and concrete manifests). Each top-level folder is a tactical or functional container. Each folder's `README.md` carries constraint authority equal to a skill file. Read it before invoking skills from that folder; it defines scope, valid placement, and routing rules for its subtree.

## [PUBLIC] Lineage

- **Canonical public snapshot:** `https://github.com/graphedge/SkillStack`. If this workspace is that clone, you are reading the allowed PromptStack corpus (not an outside repository).
- **Private operator source:** SkillStack2 authors skills and exports this tree. It is not in this snapshot. Do not fetch SkillStack2 unless the operator authorizes.
- **Kernel operator id:** see root `kernel.json` `id` field (export filter name only). OpenClaw, Hermes, Grokbot, and Cursor are harness roles on this same snapshot.

## [PUBLIC] Placement

- **Level 1**: `board/` — governance personas and stratification review workflow.
- **Level 2**: `project-classes/` (domain verticals), `core-operations/` (cross-cutting utilities).
- **Level 3**: `skill-flows/` ships NON-CANON customer fill-ins only.
- **Engine / operator indexes**: `skillstack/` has no engine files here. `verify/` ships NON-CANON customer fill-ins only.
- **NON-CANON**: `flows/samples/` and `sumplan/` are examples. They MUST NOT override Board, writing canon, or the snapshot root README.

## [PUBLIC] Constraints

- Never pull information from repositories outside this snapshot unless you have asked the operator and they have authorized it.
- PromptStack is this snapshot attached to a harness (OpenClaw, Hermes, Cursor, or similar). It is not a named agent.
- **Missing-hop gate (MUST):** If a named file or skill is not in this snapshot, stop. Do not invent it. Do not fetch another repository. This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator.
- **Sample gate (MUST):** Customer fill-in files are NON-CANON shape examples. MUST NOT treat them as Board, writing, or snapshot law. Replace them with your own rules.
- **Fast path (MUST):** Local tweak (one file, no new skill, no DNA change): edit the file and give a one-line verdict. MUST NOT run the Board sequence or the full proposal template.
- Skills MUST be stateless; required state passes explicitly through inputs and outputs.
- Shared behavior used across project classes MUST elevate to `core-operations/` or a documented shared path.
- Architecture proposals MUST pass Skeptic lenses: necessity, placement, depth. Routine fast-path edits MUST NOT be escalated into a Board play.
- Apply `-ex` vs `-mod` here: `-ex` MUST NOT modify governing files; `-mod` amends DNA before new L3 manifests. The `mode-selection` file here is a NON-CANON customer fill-in, not law.

## [PUBLIC] Children

| Folder | Role |
|--------|------|
| [board/](board/README.md) | Level 1 governance (personas + workflow) |
| [core-operations/](core-operations/README.md) | Level 2 writing canon + operator loop |
| [project-classes/](project-classes/README.md) | Level 2 placement index (no class charters here) |
| [skill-flows/](skill-flows/README.md) | Level 3 NON-CANON customer fill-ins |
| [skillstack/](skillstack/README.md) | Engine placement index (no engine files here) |
| [verify/](verify/README.md) | Audit index + NON-CANON customer fill-ins |
| [sumplan/SKILL.md](sumplan/SKILL.md) | NON-CANON handoff example |
| [flows/samples/](flows/samples/cli-config.md) | NON-CANON sample flows |
| `agent-utilities/` | This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. Optional fill-in: one block per subagent (`id`, `status`, `result` or `blocker`). |

## [PUBLIC] References

- Runtime authority is the snapshot root README (precedence stack). The constitution is not in this snapshot.
- Operator loop: [core-operations/stratification-protocol.md](core-operations/stratification-protocol.md)
- Board review sequence: [board/workflow.md](board/workflow.md)

