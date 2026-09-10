
# Core Operation: AI-Citable Content

## 1. Skill Signature

Structure an article for clear AI parsing and citation while preserving truth, source provenance, reader value, and the author's voice.

## 2. Rationale

The source image, **The AI-Citable Content Recipe** from LinkedIn for Marketing, reports that top LinkedIn articles commonly share recognizable structural features. This skill turns those observations into writing guidance without treating correlation as causation or structure as a substitute for expertise.

The source's “Structural Must-Haves” are reported frequencies, not universal requirements:

| Feature | Source-reported frequency |
|---|---:|
| Bullet Lists & Numbered Items | 100% |
| Clear H2/H3 Section Headings | 92% |
| Names Specific Companies/Tools | 75% |
| Includes Hard Numbers & Data | 65% |
| Comparison or Evaluation Framework | 50% |
| “How to Choose” Decision Guide | 33% |
| Year in Title (2025/2026) | 25% |

Use the high-frequency features as strong defaults. Use lower-frequency features only when they serve the article's claim and reader task. Never add names, numbers, comparisons, or dates merely to imitate a pattern.

**Learning value**: teaches authors to make useful claims easy to find and verify without gaming retrieval systems.

**Skeptic review**: Needs evaluation. The image reports an association without methodology, sample definition, or causal evidence.

## 3. Input-Schema

```json
{
  "topic": "string",
  "primary_claim": "string | null",
  "audience": "string",
  "target_platform": "linkedin | x_article | blog | documentation",
  "publish_lane": "personal | project",
  "draft_path": "string | null",
  "source_paths": ["string"],
  "named_companies_or_tools": ["string"],
  "hard_numbers_or_data": [
    {
      "value": "string",
      "source": "string"
    }
  ],
  "comparison_candidates": ["string"],
  "decision_required": "boolean",
  "freshness_year": "number | null",
  "voice_profile_path": "string | null"
}
```

## 4. Output-Schema

```json
{
  "status": "PASS | PASS_WITH_WARNINGS | NEEDS_REVISION",
  "outline": {
    "title": "string",
    "hook": "string",
    "sections": [
      {
        "heading": "string",
        "heading_level": "H2 | H3",
        "purpose": "string",
        "body_points": ["string"]
      }
    ],
    "lists_used": "boolean",
    "comparison_framework": "string | null",
    "decision_guide": "string | null"
  },
  "citation_ready_claims": [
    {
      "claim": "string",
      "source": "string | null",
      "status": "sourced | needs_source | opinion"
    }
  ],
  "structure_lint": {
    "bullet_or_numbered_items": "pass | warn",
    "clear_h2_h3_headings": "pass | warn",
    "specific_companies_or_tools": "pass | not_applicable | warn",
    "hard_numbers_and_data": "pass | needs_provenance | not_applicable",
    "comparison_or_evaluation": "pass | not_applicable | warn",
    "how_to_choose_guide": "pass | not_applicable | warn",
    "year_in_title": "pass | not_applicable | warn"
  },
  "confidence_note": "string",
  "next_action": "publish_review | add_sources | revise_structure"
}
```

## 5. Execution-Logic

### Step 1: Establish the claim

1. Identify one primary claim and the reader's task.
2. If the claim cannot be stated clearly, return `NEEDS_REVISION`; do not compensate with formatting.
3. Load `voice_profile_path` only when supplied and permitted by the publication lane.
4. Keep AI-citability separate from factual correctness, expertise, and voice.

### Step 2: Build the structure

1. Give the article a descriptive title and a direct opening.
2. Organize the argument with clear H2/H3 headings that state what each section answers.
3. Use bullets or numbered items for sequences, criteria, comparisons, or dense facts.
4. Name specific companies or tools when they are materially relevant to the claim. Explain their relevance.
5. Include hard numbers or data only when `source_paths` or an explicit source is supplied. Label estimates, ranges, and author analysis.
6. Add a comparison or evaluation framework when the topic contains alternatives.
7. Add a “How to Choose” decision guide when the reader must select among options.
8. Add a year to the title only when freshness changes the answer and the year is defensible.

### Step 3: Check citation readiness

For each non-obvious factual claim:

- attach a source path or mark `needs_source`;
- distinguish source fact, calculation, inference, and opinion;
- preserve enough context for a reader or agent to verify it;
- do not fabricate citations, statistics, company claims, or dates.

### Step 4: Run the structural lint

Evaluate each of the seven source features. `not_applicable` is valid for conditional features; it is not a failure. A warning is required when a feature is forced, unsupported, or structurally present but semantically unhelpful.

Use `@dependency(.github/skills/core-operations/writing/writing-standards.md)` for anti-AI-smell, sentence-shape, and platform-length checks. Output acceptance checks are operator-local (not in this kernel).

### Step 5: Return the review result

- `PASS` when the structure serves the claim, factual claims are sourced or clearly labeled, and no forced-pattern warning remains.
- `PASS_WITH_WARNINGS` when the article is usable but has minor structural or provenance gaps.
- `NEEDS_REVISION` when the primary claim is unclear, evidence is missing for central claims, or optimization has displaced reader value.

This skill drafts or reviews content. It does not publish, alter voice profiles, or guarantee that an AI system will cite the article.

## 6. Anti-Gaming Rules

- Do not keyword-stuff company or tool names.
- Do not invent hard numbers to satisfy the recipe.
- Do not add comparison tables when no meaningful alternatives exist.
- Do not add a decision guide when the article has no reader decision.
- Do not add a year merely because the source image lists one.
- Do not use headings that promise an answer the section does not provide.
- Do not confuse clean structure with truth, authority, originality, or citation likelihood.
- Do not claim the source percentages predict performance; they are source-reported observations.

## 7. Writing-Layer Integration

This is a shared Core Operations writing skill:

- [`writing-standards.md`](writing-standards.md) owns anti-AI-smell, sentence shape, and platform length.
- [`harness-advice.md`](harness-advice.md) owns vendor/repo harness terminology and compose routing.
- [`preference-inference.md`](preference-inference.md) supplies optional author preferences.
- A publication voice profile (operator-local) supplies audience and content artifacts.
- Variant evaluation after composition is **not in this kernel**; it does not replace this structural pass.

Workflow:

```text
topic + sources + voice profile
        ↓
ai-citable-content
        ↓
writing-standards
        ↓
harness-advice / publication-voice lane
        ↓
evaluate (not in this kernel)
```

Reusable logic belongs here, not in operator-local `specs/prompts/<slug>/` voice or publication material.

## 8. Source and Governance Notes

**Source**: `prompts/AIfirst-articles.png` (not in this snapshot; do not fetch it unless the operator authorizes).  
**Source title**: *The AI-Citable Content Recipe*  
**Source publisher**: LinkedIn for Marketing  
**Source framing**: “The top LinkedIn articles share a practical structure AI loves.”

The seven percentages are source-reported heuristics and descriptive observations. The image does not disclose methodology, sample size, selection criteria, or whether “citable” means retrieval, quotation, ranking, or another outcome. Preserve that uncertainty in any downstream draft.

This skill must remain stateless. It may read supplied source artifacts and draft content, but it must not persist hidden learning, modify publication history, or auto-promote outputs.

---

**Dependency Links**: `@dependency(.github/skills/core-operations/writing/writing-standards.md)`, `@dependency(.github/skills/core-operations/writing/harness-advice.md)`. QA and state-management skills are not in this kernel.  
**Skeptic Review**: Needs evaluation  
**Status**: Draft  
**Owner**: SkillStack  
**Path**: `.github/skills/core-operations/writing/ai-citable-content.md`
