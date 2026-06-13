# OpenCode Guidelines

A 4-layer Agent OS configuration for [opencode](https://opencode.ai), designed for Spec-Driven Development and structured tool usage.

## Architecture

| Layer | File | Responsibility |
|---|---|---|
| **Behavior** | `AGENTS.md` | Communication style, core principles, conditional loading rules |
| **Workflow** | `SDD_MANUAL.md` | Spec-Driven Development lifecycle and artifact management |
| **Capability** | `TOOL_MANUAL.md` | Git workflow, package managers, testing strategy, tool selection, CodeGraph usage |
| **Artifact** | `templates/*.template.md` | Minimal skeletons for PRD / Plan / Task / Spec / Checklist |

## Usage

Copy the entire directory to `~/.config/opencode/`:

```bash
cp -r ./* ~/.config/opencode/
```

Or cherry-pick individual files as needed.

### How It Works

- `AGENTS.md` is always loaded as the core behavior rules — it stays under 40 lines.
- `SDD_MANUAL.md` and `TOOL_MANUAL.md` are loaded **on demand** via conditional loading rules in `AGENTS.md`.
- Templates provide 70% skeletons — AI expands them based on actual task complexity.

## Design Principles

1. **Single Source of Truth** — `AGENTS.md` is the authority. Workflow and Capability files extend, never contradict.
2. **Conditional Loading** — Avoid context pollution. Load only what the task requires.
3. **Minimal Skeletons** — Templates define structure, not content. No empty boilerplate.
4. **Extensible** — New tools, workflows, or template variants slot into their layer without modifying other files.

## Contents

```
~/.config/opencode/
├── AGENTS.md            # Core behavior rules + conditional loading
├── SDD_MANUAL.md        # Spec-Driven Development workflow
├── TOOL_MANUAL.md       # Git, package managers, testing, CodeGraph
└── templates/
    ├── prd.template.md
    ├── plan.template.md
    ├── task.template.md
    ├── spec.template.md
    └── checklist.template.md
```

## License

MIT