
# Core Operation: Signal Amplification

**Invoke:** `-ex @signal-amplification` · turn friction posts into repo-harness drafts

## Overview

Identifies high-engagement friction signals from social platforms and decomposes them into branding opportunities. Convert engineering frustration (nerfs, failures, lock-ins) into repo-harness advocacy.

## Goal

1. Deconstruct the friction hook of a viral post.
2. Map the frustration to a specific inadequacy in vendor harnesses.
3. Draft a pivot post that positions the repo harness as the solution.

## Behavior

1. **Signal Extraction**: Fetch content from `target_url`.
2. **Friction Scan**: Search for high-intent keywords:
   - `nerfed`, `safety rails`, `lock`, `error`, `refuse`, `unfunny`, `stupid`, `regex`, `security nanny`, `session loss`.
3. **Deconstruction**:
   - **The Pain**: What exactly failed?
   - **The Why**: Why did it fail?
   - **The Impact**: How much work or time was lost?
4. **The Pivot**:
   - **The Contrast**: Vendor harness (cause of failure) vs repo harness (solution).
   - **The Value**: Explain how a repo-native tool (for example SpecKit or OpenSpec) prevents this friction.
5. **Drafting**: Generate a draft following `writing-standards`. Compose through `@dependency(.github/skills/core-operations/writing/harness-advice.md)` as the shared home compose skill. Bind author voice from a local profile, not from names in this file.

## Input Requirements

- `target_url` (Required): URL of the post.
- `specialization` (Optional): project handle key (defaults unset).
- `target_platform` (Optional): `x_post` | `linkedin`.

## Output Schema

- `engagement_analysis.json`: Contains Hook, Friction Type, and Intensity.
- `amplification_draft.md`: The finalized post ready for review.

## Dependency Links

- `writing-standards`
- `@dependency(.github/skills/core-operations/writing/harness-advice.md)` — home compose skill
- Voice profile: `specs/prompts/<slug>/voice_preference_profile.json` (operator-local)

## Rationale

Capitalizes on high-intensity engineering pain to drive authority and brand awareness for the repo-native ecosystem.
