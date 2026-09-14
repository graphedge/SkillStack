
# Core Operation: Preference Inference

## 1. Skill Signature

Infer author voice preference profile from assistant draft vs author nearfinal diff; emit reusable JSON for harness-advice compose and operator-local evaluator profile alignment.

## 2. Rationale

An operator-local evaluator (not in this kernel) compares variants to a voice anchor transcript but does not extract reusable compose rules from author edits. This skill closes the gap: human nearfinal edits become a `voice_preference_profile` that harness-advice loads on the next draft.

**Skeptic Review:** Approved — third writing child; keeps voice prefs out of writing-standards structural lint.

## 3. Input-Schema

```json
{
  "assistant_draft_path": "string (path to assistant-produced draft body)",
  "author_nearfinal_path": "string (path to author-edited nearfinal)",
  "voice_anchor_path": "string (optional; strengthens idiom and signature phrase detection)",
  "slug": "string (e.g. publication-slug; used for output path)"
}
```

## 4. Output-Schema

```json
{
  "profile_path": "string (artifacts/writing/preference-inference/{slug}/voice_preference_profile.json or specs/prompts/{slug}/)",
  "voice_preference_profile": {
    "version": "1.0",
    "source": {
      "assistant_draft": "string",
      "author_nearfinal": "string",
      "voice_anchor": "string | null"
    },
    "lexicon_prefer": ["string"],
    "lexicon_avoid": ["string"],
    "hedging": "string (rule description)",
    "humor": "string (rule description)",
    "framing": "string (rule description)",
    "numbers": "string (rule description)",
    "rhythm": ["string"],
    "signature_phrases": ["string"],
    "parentheticals": "string (rule description)",
    "early_grounding": "string (rule description)"
  },
  "preference_deltas": [
    {
      "category": "Lexicon | Rhythm | Framing | DomainVocab | Hedging | Numbers | Humor | Audience | Closing | EarlyGrounding",
      "assistant": "string",
      "author": "string",
      "rule": "string"
    }
  ]
}
```

## 5. Execution-Logic

1. Load `assistant_draft_path` and `author_nearfinal_path`; strip frontmatter and `## Ready to post` headers; extract body text only.
2. If `voice_anchor_path` provided, extract signature phrases (3+ word idioms, first-person markers) for merge into profile.
3. Diff bodies line-by-line and sentence-by-sentence; classify each author change into preference buckets (see **Classification buckets** below).
4. Merge classified edits into `voice_preference_profile` JSON per output schema.
5. Write `preference_deltas` array documenting each inferred rule with before/after examples.
6. Write profile to `artifacts/writing/preference-inference/{slug}/voice_preference_profile.json`. For certified golden fixtures, MAY also copy to `specs/prompts/{slug}/voice_preference_profile.json`.

**Dependency Links:**

- `@dependency(.github/skills/core-operations/writing/writing-standards.md)` — do not learn structural violations (em dash, 5+ phrases) as preferences
- Consumed by: `@dependency(.github/skills/core-operations/writing/harness-advice.md)`; optional operator-local evaluator (not in this kernel) for profile alignment
- Inventory paths for `author_nearfinal_file` / `voice_preference_profile` are operator-local (not in this kernel)

---

## Classification buckets

| Bucket | What to detect | Example rule |
|--------|----------------|--------------|
| `lexicon_prefer` | Terms author added or kept | "cloud company", "organize pre-context", first-person "us" |
| `lexicon_avoid` | Terms author removed or replaced | "closely related source", "essentially", "So I" |
| `hedging` | Epistemic softening | prefer may/might on capability claims |
| `humor` | Wry or cynical lines author added | unpaid marketing research team for a frontier lab |
| `framing` | Shorter or different dependency warnings | less crisis disclaimer; "more dependent than you need to be" |
| `numbers` | Range and framing changes | round ranges; capability not performance % |
| `rhythm` | Filler dropped, concrete detail added | drop "essentially"; add "tonight" in quotes |
| `signature_phrases` | Verbatim nearfinal phrases to preserve | multi-word idioms unique to author |
| `parentheticals` | Self-edit qualifiers | "(slightly)" OK |
| `early_grounding` | Product names moved earlier | "like Claude Code" inline in opening paras |

**Do NOT learn:**

- Typos (e.g. stray space before period)
- writing-standards HardBlock violations
- Platform or governance metadata

## Profile application (downstream)

**harness-advice** (compose): load `voice_preference_profile` when `publish_lane=personal`; apply `lexicon_prefer`, `lexicon_avoid`, `signature_phrases`, and rule strings at draft time.

**Evaluate** (operator-local, not in this kernel): optional `voice_preference_profile_path` when scoring variants; friction triggers for profile misalignment stay in that evaluator.

## Workflow position

```
assistant_draft + author_nearfinal → preference-inference → voice_preference_profile.json
voice_anchor + profile → harness-advice (draft) → writing-standards (lint) → evaluate (not in this kernel)
```

**Status:** Certified v1.0.0
