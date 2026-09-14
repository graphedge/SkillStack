## [PUBLIC] Scope

Engine skills operate the SkillStack domain model: entity registry, classification, intake, and export tooling. They are operator-facing, not Board personas. This snapshot includes [`cloud-agent-normal-route`](cloud-agent-normal-route.md) (PUBLIC Route only). Other engine skill files are not in this pack.

## [PUBLIC] Placement

Add skills here for **registry, intake, export, and repo automation**. Board governance belongs in `board/`. Generic QA belongs in `core-operations/`. Audit skills belong in `verify/`.

## [PUBLIC] Constraints

- New entities MUST be classified and registered before they are added to this tree.
- Only registered skills are canon.
- Skills MUST document invoke pattern (`-ex @skill-id` or documented CLI).
- Named engine skills are not in this snapshot except [`cloud-agent-normal-route`](cloud-agent-normal-route.md) (PUBLIC Route only). Other hops: Fast path if the task is a local edit; otherwise ask the operator.

## [PUBLIC] Children

| Skill | Purpose |
|-------|---------|
| `classify-transfer`, `intake-batch`, `project-intake` | This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. |
| `portfolio-map`, `dev-progress-status` | This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. |
| `registry-repo-commit`, `registry-followup-pr` | This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. |
| `repo-onboarding`, `repo-stack-inspect`, `speckit-bootstrap` | This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. |
| `soul-publish`, `soul-draft-review` | This pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. |
| [`cloud-agent-normal-route`](cloud-agent-normal-route.md) | Parameterized implement / assess / sol harness route. Not a Board lane. |

Feasible customer fill-in for this folder (example, not law): a one-page "how we register a skill" note — name, path, owner — with no tokens and no push scripts.

## [PUBLIC] References

- Parent: [skill tree README](../README.md)

