# AGENTS.md — Core Behavior Rules

**Single Source of Truth.** SDD_MANUAL.md and TOOL_MANUAL.md extend this file. They must never be stricter than or contradict the rules below.

## Environment

This environment is WSL2 Ubuntu 26.04 sharing a filesystem with Windows.

- **File system**: Code lives under `/mnt/c/` for Windows persistence. Prefer `/tmp/` or `~/` for temporary/build artifacts (cross-filesystem access to `/mnt/c/` is slower).
- **Paths**: Always use Linux paths (`/mnt/c/...`). Never use Windows paths (`C:\...`). Windows executables cannot be called directly.
- **Network**: WSL2 uses NAT. localhost is bidirectionally reachable. External services need the WSL-assigned IP. Windows→WSL port forwarding is automatic.
- **Line endings**: Git uses LF. Avoid CRLF when editing files from Windows tools.
- **Execution**: Ubuntu Linux native. System packages via apt. Python/Node are native Linux versions. No Wine/compatibility layer.

## Communication

- Use Chinese for conversation; code, comments, and commit messages in English.
- Be concise during implementation. Allow discussion during planning phases.

## Core Rules

1. **Don't assume requirements.** State your assumptions explicitly. If uncertain, ask.
2. **Simplest solution first.** No over-engineering, no future-proofing, no speculative features.
3. **Surgical changes.** Only modify code directly related to the task. Match existing style.
4. **Strong typing.** TypeScript: no `any`. Python: type hints on every function signature.
5. **Validate changes.** Run the relevant tests or verification steps after implementation.
6. **Explain tradeoffs.** When multiple approaches exist, present them. Don't decide silently.
7. **Use the project's defined workflow** for non-trivial development tasks.
8. **Write a minimal reproduction** before fixing a failure.

## Conditional Loading

Load external manuals only when the task requires them.

- Before Git operations (commit, branch, push), you **MUST** load `TOOL_MANUAL.md`.
- Before creating or modifying PRD / Plan / Task / Spec / Checklist, you **MUST** load `SDD_MANUAL.md`.
- When a task requires knowledge not in this file, load the smallest relevant manual before acting.
- Never load unrelated manuals.