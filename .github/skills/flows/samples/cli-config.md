
# Skill Flow: CLI Alias Configuration (Developer Tools)

**NON-CANON.** Sample flow. MUST NOT override Board, writing canon, or the snapshot root README.

## 1. Skill Signature

Configures project-specific CLI aliases and environment variables to streamline developer workflows.

## 2. Rationale

Manual environment setup is error-prone and slows down onboarding. This skill automates the creation of a standardized local toolchain.
Learning Value: Teaches the user how to manage shell environments without polluting global configs.

## 3. Input-Schema

```json
{
  "required_aliases": "object",
  "env_vars": "object",
  "shell_type": "string"
}
```

## 4. Output-Schema

```json
{
  "config_file_path": "string",
  "activation_command": "string",
  "verification_status": "boolean"
}
```

## 5. Execution-Logic

1. **Shell Detection**: Validate `shell_type` (bash/zsh/fish).
2. **Config Generation**: Write the aliases and env vars to a project-local `.envrc` or similar shell-specific file.
3. **Dependency Check**: Generate a "How to use this toolchain" guide (documentation skill is not in this kernel).
4. **Verification**: Execute the aliases to ensure they resolve to the correct binaries.

---
**Dependency Links**: documentation and QA skills are not in this kernel.
**Skeptic Review**: Approved
**Status**: Certified
