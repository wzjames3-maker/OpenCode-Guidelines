# SDD_MANUAL — Spec-Driven Development Workflow

## Overview

SDD (Spec-Driven Development) is the standard workflow for non-trivial development tasks.

```
Idea → PRD → Plan → Task → Spec → Checklist → Implement → Test → Deploy
```

## Artifact Dependency

Each artifact builds on the previous one. Missing artifacts must be created before proceeding.

```
Idea
  ↓
PRD          — what problem to solve, for whom
  ↓
Plan         — how to approach, major milestones
  ↓
Task         — single unit of implementable work
  ↓
Spec         — precise behavioral contract
  ↓
Checklist    — pass/fail criteria for this task
  ↓
Implementation
```

### Constraints

- Every Task must have a corresponding Spec.
- Every Spec must have a corresponding Checklist.
- Implementation must not begin without a current Task.
- Large requests must be decomposed: Idea → Plan, then each Plan step → Task.
- Trivial changes (typos, formatting, single-line fixes, dependency bumps) may skip this workflow.

## Template Locations

All templates are stored in `~/.config/opencode/templates/`. Output to project root:

| Artifact | Template |
|---|---|
| PRD | `~/.config/opencode/templates/prd.template.md` → `prds/` |
| Plan | `~/.config/opencode/templates/plan.template.md` → `plans/` |
| Task | `~/.config/opencode/templates/task.template.md` → `tasks/` |
| Spec | `~/.config/opencode/templates/spec.template.md` → `specs/` |
| Checklist | `~/.config/opencode/templates/checklist.template.md` → `checklists/` |

## Implementation Flow

1. Locate the current Task.
2. Read the corresponding Spec.
3. Read the corresponding Checklist.
4. Implement according to the Spec.
5. Update the Checklist after implementation.

## Completion Criteria

A Task is complete only if:

- Implementation matches the Spec.
- All Checklist items are complete.
- Tests pass.
- Related documents have been updated.

## Context Management

- During implementation, prioritize: Current Task → Current Spec → Current Checklist.
- Load templates only when creating or updating the corresponding artifact.
- Never load unrelated documents.
