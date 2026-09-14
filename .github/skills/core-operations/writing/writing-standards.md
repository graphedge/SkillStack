
# Core Operation: Writing Standards

## 1. Skill Signature

Enforce compose-side writing rules for social and long-form drafts: anti-AI-smell lint, run-on phrase targets, and quantitative platform length targets.

## 2. Rationale

An operator-local evaluator (not in this kernel) scores voice verisimilitude but had no upstream compose constraints. This parent overskill supplies shared lint rules for harness-advice (compose) and that evaluator. Project lane uses soft flags; personal lane uses hard blocks.

**Skeptic Review:** Approved — fills gap left by a private upstream skill that referenced a nonexistent brand-voice Core Op.

## 3. Input-Schema

```json
{
  "draft_path": "string (path to draft markdown)",
  "target_platform": "linkedin | x_post | x_thread | x_article",
  "publish_lane": "personal | project (default: personal)",
  "lint_only": "boolean (default: true — report violations without rewriting)"
}
```

## 4. Output-Schema

```json
{
  "lint_report": {
    "platform": "string",
    "word_count": "number",
    "char_count": "number",
    "within_length_target": "boolean",
    "violations": [
      {
        "rule": "EmDash | ContrastGimmick | AssistantMeta | EmojiHeader | RunOn5Plus | RunOn4Density | LengthOutOfRange",
        "severity": "HardBlock | SoftFlag",
        "line_hint": "string",
        "description": "string"
      }
    ],
    "platform_fit_penalty": "number (sum of evaluator Platform Fit deductions)"
  },
  "pass": "boolean"
}
```

## 5. Execution-Logic

1. Load draft; strip YAML frontmatter and markdown headers before counting body length.
2. Apply **Anti-AI-smell rules** (see below).
3. Apply **Run-on adjustment rule** (see below).
4. Count words/chars; compare to **Platform length targets** for `target_platform`.
5. Emit `lint_report`; `pass=true` when no HardBlock violations remain.

**Dependency Links:**

- Manifest schema and `artifacts/` convention: operator-local documentation skill (not in this kernel)
- Consumed by: `@dependency(.github/skills/core-operations/writing/harness-advice.md)`; optional operator-local evaluator (not in this kernel)

---

## Anti-AI-smell rules

| Rule | Personal lane | Project lane | Fix |
|------|---------------|--------------|-----|
| **No em dash** (`—`, `–`) | HardBlock | SoftFlag | Period, comma, or split sentence |
| **No contrast gimmicks** ("This Not That", stacked "not X but Y") | HardBlock | SoftFlag | State claim directly |
| **No assistant-to-author framing** | HardBlock | HardBlock | Strip meta wrappers |
| **No emoji section headers** | HardBlock | SoftFlag | Plain text headers |
| **Run-on adjustment** | HardBlock at 5+ | SoftFlag at 5+ | See below |
| **Short paragraphs** | SoftFlag | SoftFlag | 1–3 sentences on social platforms |

**Assistant-to-author examples (HardBlock):** "Got it — thanks for sharing", "Here's a polished version", "If you want, I can also produce".

---

## Run-on adjustment rule

**Target:** 1–3 phrases per sentence in most cases.

**Allow** occasional 4-phrase sentences for natural rhythm or emphasis, but **never 5+**.

**Heuristic:**

A phrase = independent clause or subject-verb unit separated by comma, semicolon, or coordinating conjunction.

**3 phrases (acceptable):**

> I tried the new harness, it felt powerful at first, and the results were impressive.

**4 phrases (allowed sparingly):**

> I loaded the voice anchor, applied the standards, ran the draft through the evaluator, and the score jumped nicely.

**5+ phrases (flag / split):**

> I opened the file, read the prompt, loaded the anchor, applied the rules, checked the length, and then published it.

**Lint thresholds:**

| Count | Action |
|-------|--------|
| 1–3 phrases | PASS |
| 4 phrases | PASS if ≤10% of sentences; else SoftFlag `RunOn4Density` |
| 5+ phrases | HardBlock `RunOn5Plus` — split required |

---

## Platform length targets

| Platform | `target_platform` | Body target | Hard max | Structure notes |
|----------|-------------------|-------------|----------|-----------------|
| LinkedIn | `linkedin` | 400–550 words (~2,400–3,300 chars) | 700 words | Fold hook ≤210 chars; 1 CTA question; 0–3 hashtags optional |
| X post | `x_post` | 220–260 chars | 280 chars | Single post; 1 idea; no thread numbering |
| X thread | `x_thread` | 6–10 tweets × 200–260 chars each | 15 tweets | Tweet 1 = hook; last tweet = CTA; each tweet ≤280 |
| X article | `x_article` | 700–1,000 words | 1,500 words | H2 every 150–200 words; no em dash |

---

## Evaluator Platform Fit penalties (personal lane)

Apply when an operator-local evaluator (not in this kernel) scores Platform Fit. Reference this table; do not duplicate in that evaluator.

| Violation | Penalty |
|-----------|---------|
| Body outside target range for `target_platform` | −2.0 |
| Any em dash | −1.5 per occurrence (cap −3.0) |
| Any 5+ phrase sentence | −1.5 per occurrence (cap −3.0) |
| 4-phrase sentences beyond ~10% of total sentences | −0.5 per excess |
| Assistant meta wrapper | Auto-fail Assistant Contamination dimension |

---

## Compose vs evaluate split

| Concern | Owner | When |
|---------|-------|------|
| Voice anchor, signature phrases | operator-local evaluator (not in this kernel) | Evaluate |
| Anti-AI-smell, length, sentence shape | **writing-standards** | Compose + evaluate |
| Harness taxonomy accuracy | harness-advice | Compose |
| Hybrid format/voice donor | operator-local evaluator (not in this kernel) | Evaluate |

**Status:** Certified v1.0.0
