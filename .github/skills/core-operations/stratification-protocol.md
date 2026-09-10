## [PUBLIC] Scope

This skill is the operator loop for turning an objective into Board-reviewed, placed skill manifests.

**Invoke:** `-ex @stratification-protocol` · stratification viability manifest proposal

It does not replace Board personas: [board/workflow.md](../board/workflow.md) remains the three-stage review sequence for architecture. Linked `recursive-decomposition` and `manifest-generation` files in this snapshot are NON-CANON customer fill-ins, not required hops.

## [PUBLIC] Fast path

**MUST** use this path when the change is a local tweak (one file, no new skill, no DNA change):

1. Edit the file.
2. State a one-line verdict.
3. Stop.

MUST NOT run the Board sequence or the proposal template below. MUST NOT escalate routine work into a Board play.

## [PUBLIC] Protocol

Required first step: apply `-ex` vs `-mod` here. `-ex` MUST NOT edit governing files. `-mod` amends DNA before new L3 manifests. The `mode-selection` file in this snapshot is a NON-CANON customer fill-in, not law.

Operational (`-ex`) sequence for architecture (not fast path):

1. **Viability** — Outside Board framing, list pros, cons, and a verdict (proceed / pivot / stop).
2. **Decomposition** — Run Board lenses (Strategy Lead → Pivot Lead → Skeptic). Map to Level 2: project class and/or core operation. Each stage MUST write a named artifact.
3. **Manifests** — For each new skill, write invoke, inputs, outputs, and rationale in-line. The `manifest-generation` fill-in is an example shape only.
4. **Recursive split** — If a skill is oversized, write a text tree and a one-line depth note. The `recursive-decomposition` fill-in is an example shape only.
5. **Folder tree** — Propose paths; prefer flat clarity; add depth only when it reduces load.
6. **Skeptic pass** — Explicit necessity, placement, and depth on the whole proposal.
7. **Progressive disclosure** — Simple work stays in one file; deeper folders only when complexity warrants.

If a named hop is not in this snapshot: this pack does not include that hop. Fast path if the task is a local edit; otherwise ask the operator. Do not invent it.

## [PUBLIC] Proposal format

**MUST** use these headings for non-trivial architecture proposals. Fast path (above) has equal force and MUST win for routine edits.

```markdown
**Board directive**:

**Real-world viability**
- Pros:
- Cons:
- Verdict:

**Level 2 alignment**:

**Skill flow architecture**:

**Recommended folder structure**:

**Skeptic review**
- Necessity:
- Placement:
- Depth:

**Why this hierarchy + learning takeaway**:

**Next actionable manifests**:
```

## [PUBLIC] Constraints

- Every generated skill yields a direct action (code, manifest, decision) or a documented priority change.
- Major responses name the architectural trade-off and the lesson for the next design.
- Skills are stateless; state passes through inputs and outputs.
- Behavior used across project classes elevates to `core-operations/` or a documented shared path.
- One `board/` with one file per persona; parallel `project-classes/` and `core-operations/` at Level 2; execution under `skill-flows/` or class-specific subtrees.
- Customer fill-ins are NON-CANON. Samples under `flows/samples/` and `sumplan/` are examples, not law.

## [PUBLIC] References

- Board review sequence: [board/workflow.md](../board/workflow.md)
- Skill tree orientation: [../README.md](../README.md)
- This folder: [README.md](README.md)

