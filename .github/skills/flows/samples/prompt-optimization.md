
# Skill Flow: Prompt Template Optimization (AI Engineering)

**NON-CANON.** Sample flow. MUST NOT override Board, writing canon, or the snapshot root README.

## 1. Skill Signature

Optimizes LLM prompt templates for token efficiency and response accuracy using a recursive feedback loop.

## 2. Rationale

Poorly structured prompts waste tokens and produce inconsistent results. This skill standardizes the process of refining prompts through iterative testing.
Learning Value: Teaches the user about few-shot prompting and prompt-versioning.

## 3. Input-Schema

```json
{
  "initial_prompt": "string",
  "target_metrics": "object",
  "sample_inputs": "array"
}
```

## 4. Output-Schema

```json
{
  "optimized_prompt": "string",
  "token_reduction_percentage": "number",
  "accuracy_gain": "number"
}
```

## 5. Execution-Logic

1. **Baseline Measurement**: Execute `initial_prompt` against `sample_inputs` and measure `target_metrics`.
2. **Iterative Refinement**: Apply prompt engineering techniques (e.g., chain-of-thought, clear constraints).
3. **Verification**: Repeat baseline measurement for each variant.
4. **State Transition**: Record the prompt version history (state-management skill is not in this kernel).

---
**Dependency Links**: state-management and QA skills are not in this kernel.
**Skeptic Review**: Approved
**Status**: Certified
