
# Core Operation: Harness Advice

**Invoke:** `-ex @harness-advice` · compose vendor vs repo harness drafts

## 1. Skill Signature

Advise on AI harness taxonomy and draft platform-native posts about vendor vs repo harnesses with writing-standards compliance.

## 2. Rationale

Authors confuse colloquial terms ("cloud code") with product names (Claude Code) and mix vendor harnesses with repo-native frameworks. This skill supplies correct taxonomy and drafts posts that pass writing-standards lint.

### Home identities (placeholders)

Same skill; platform and voice inputs differ. Bind real author names and handles in a local voice profile — not in this file.

| Channel | Identity | Typical lane / voice |
|---------|----------|----------------------|
| Professional network | `<Author Name>` | `publish_lane=personal` (+ voice anchor / preference profile) |
| Short-form social | `<@handle>` | `publish_lane=project` (or project voice via `specs/prompts/<slug>/voice_preference_profile.json`) |

Do not treat a display-name difference across channels as a reason to invent private linkage in this skill.

## 3. Input-Schema

```json
{
  "publish_lane": "personal | project",
  "target_platform": "linkedin | x_post | x_thread | x_article",
  "voice_anchor_path": "string (required when personal)",
  "voice_preference_profile_path": "string (optional; from preference-inference)",
  "topic": "string",
  "audiences": ["righteous_strugglers", "unhelpful_addiction", "beginners"],
  "tone": "balanced | invitation (default: balanced, not crisis-driven)"
}
```

## 4. Output-Schema

```json
{
  "draft_path": "string (artifacts/harness-advice/{slug}/{n}/draft_{platform}.md)",
  "lint_report": "object (from writing-standards)",
  "harness_terms_used": ["string"],
  "pass": "boolean"
}
```

## 5. Execution-Logic

1. `@dependency(.github/skills/core-operations/writing/writing-standards.md)` — load compose rules before drafting.
2. If `publish_lane=personal`, load `voice_anchor_path`; preserve signature phrases and first-person rhythm.
3. If `voice_preference_profile_path` is provided, load profile and apply `lexicon_prefer`, `lexicon_avoid`, `signature_phrases`, and the listed rule strings.
4. Draft using **Harness taxonomy** below; apply **Tone defaults**.
5. Self-lint via writing-standards: em-dash scan, phrase-count, word/char count vs platform table.
6. Write output to `artifacts/harness-advice/{slug}/{n}/draft_{platform}.md`.

**Dependency Links:**

- `@dependency(.github/skills/core-operations/writing/writing-standards.md)` — compose lint (required)
- `@dependency(.github/skills/core-operations/writing/preference-inference.md)` — voice preference profile (optional; personal lane)
- Variant evaluation after draft is **not in this kernel**. Do not copy private evaluator paths into a public export.

---

## Harness taxonomy

Use correct product names. Never use "cloud code" or "cloud desktop" as generic terms.

| Colloquial / wrong | Correct term | Class |
|--------------------|--------------|-------|
| cloud code | **Claude Code** | vendor harness (Anthropic terminal/IDE agent) |
| cloud desktop | **Claude Desktop** | vendor harness (Anthropic desktop app) |
| ChatGPT Desktop / Work | same | vendor harness (OpenAI) |
| Codex | absorbed into ChatGPT Desktop/Work | vendor harness (historical) |
| DSPy, SpecKit, OpenSpec, Ralph loop | repo harnesses | model-agnostic, portable |

**Vendor harness:** tooling bundled with or optimized for a single model vendor.

**Repo harness:** frameworks in the repo that wrap work and port across environments.

When comparing classes, name vendors explicitly (Claude Code, Claude Desktop, ChatGPT Work) rather than "cloud" abstractions.

---

## Tone defaults

- Acknowledge people using frontier vendor tools productively without crisis framing.
- Frame dependency as flexibility risk, not moral failure.
- Scope "unhelpful addiction" as a smaller subset, not the default reader.
- Avoid em dash; use periods or commas per writing-standards.

## Audience segments (optional)

| Key | Description |
|-----|-------------|
| `righteous_strugglers` | Building long-imagined software; valid drive, needs sustainable scaffolding |
| `unhelpful_addiction` | Cannot sleep while model access is available; smaller group |
| `beginners` | New or frustrated; not behind, just early |

## Voice preference profile (personal lane)

When a `voice_preference_profile_path` is loaded, apply in addition to tone defaults:

| Profile field | Compose action |
|---------------|----------------|
| `lexicon_prefer` | Use these terms over generic alternatives |
| `lexicon_avoid` | Do not use; replace per profile deltas |
| `signature_phrases` | Preserve verbatim when topic fits |
| `hedging` | Soften capability claims (may/might) |
| `humor` | Allow wry vendor critique when grounded |
| `framing` | Shorter dependency warnings; less crisis disclaimer |
| `numbers` | Round capability ranges; capability not performance framing |
| `early_grounding` | Name Claude Code or flagship vendor harness in opening paragraphs |

Golden profile path is operator-local: `specs/prompts/<slug>/voice_preference_profile.json`.

## Workflow position

```
voice_anchor + voice_preference_profile → harness-advice (draft) → writing-standards (lint) → evaluate (not in this kernel) → final_publish.md
```

**Status:** Certified v1.1.0 (public placeholder; no author PII)
