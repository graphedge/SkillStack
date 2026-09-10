
# Skill Flow: PLC Logic Validation (Manufacturing)

## 1. Skill Signature

Validates PLC (Programmable Logic Controller) logic outputs against safety and operational specifications.

## 2. Rationale

In manufacturing, a logic error can lead to hardware damage or safety incidents. This skill provides a rigorous way to verify PLC code before deployment.
Learning Value: Teaches the user how to map high-level safety requirements to boolean logic checks.

## 3. Input-Schema

```json
{
  "plc_code_snippet": "string",
  "safety_specs": "object",
  "test_vectors": "array"
}
```

## 4. Output-Schema

```json
{
  "validation_result": "PASSED | FAILED",
  "error_log": "array",
  "coverage_report": "object"
}
```

## 5. Execution-Logic

1. **Requirement Mapping**: Parse `safety_specs` to identify critical safety interlocks.
2. **Static Analysis**: Analyze `plc_code_snippet` for common logic errors (e.g., race conditions, unhandled states).
3. **Vector Testing**: Run the `test_vectors` through the logic to verify expected outputs.
4. **QA Certification**: Certify the result against the "Definition of Done" (QA skill is not in this kernel).

---
**Dependency Links**: QA and state-management skills are not in this kernel.
**Skeptic Review**: Approved
**Status**: Certified
