
# Verification Skill: PDF Report Review

**Invoke:** `-ex @pdf-report-review` · after generating a PDF, before delivery

## 1. Skill Signature

Inspect rendered PDF pages for offsets, clipping, overflow, blank space, legibility, and page-target compliance. This is a **render review**, not a content fact-check.

## 2. Rationale

A PDF can exist with the right page count and still be undeliverable: wrapped bullet continuations jump to the far right, body clips the margin, headings strand above empty space. Byte existence and extracted text are not visual pass.

**Skeptic:** Necessity pass (layout bugs ship when agents stop at file-write); Placement pass under `verify/core/` beside other compliance audits; Depth pass when limited to render QA (no rewrite of the briefing’s facts).

## 3. Input-Schema

```json
{
  "pdf_path": "string",
  "page_target": "number | null",
  "reference_image": "string | null"
}
```

## 4. Output-Schema

```json
{
  "overall": "Pass | Soft fail | Hard fail",
  "page_count": "number",
  "findings": [
    {"page": "number", "severity": "Soft fail | Hard fail", "region": "string", "fix": "string"}
  ],
  "safe_to_deliver": "boolean"
}
```

## 5. Execution-Logic

1. Verify the file opens. If `page_target` is supplied, page count must match.
2. Render each page to an image (or inspect with a PDF-capable visual tool) at normal zoom.
3. Check every page for:
   - text shifted outside margins or into another column
   - wrapped bullet continuation detached from its bullet
   - clipping at right/bottom edge
   - headers/footers colliding with body
   - stranded headings / giant unexplained white gaps
   - text too small for normal mobile/desktop reading
4. Compare to authoring intent or `reference_image` if supplied.
5. Return Pass / Soft fail / Hard fail with page + region hints. **Hard fail** any clipped or off-page body text.
6. Never claim visual pass from PDF byte existence or extracted text alone.
7. If review is Hard fail, do not deliver the PDF with a caveat; regenerate after a layout fix.
