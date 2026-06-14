# OpenCode Guidelines

一套为 opencode 设计的四层 Agent OS 配置，面向 Spec-Driven Development 和结构化工具使用。

A 4-layer Agent OS configuration for [opencode](https://opencode.ai), designed for Spec-Driven Development and structured tool usage.

---

## 架构 / Architecture

| 层 Layer | 文件 File | 职责 Responsibility |
|---|---|---|
| **行为层 Behavior** | `AGENTS.md` | 沟通规范、核心原则、条件加载路由 / Communication style, core principles, conditional loading rules |
| **工作流层 Workflow** | `SDD_MANUAL.md` | SDD 全流程与工件管理 / Spec-Driven Development lifecycle and artifact management |
| **能力层 Capability** | `TOOL_MANUAL.md` | Git、包管理器、测试、CodeGraph / Git workflow, package managers, testing, CodeGraph |
| **产出层 Artifact** | `templates/*.template.md` | PRD/Plan/Task/Spec/Checklist 最小骨架 / Minimal skeletons for each artifact |

---

## 使用方式 / Usage

复制到 `~/.config/opencode/`：

```bash
cp -r ./* ~/.config/opencode/
```

也可按需选取单个文件。Or cherry-pick individual files as needed.

### 如何工作 / How It Works

- `AGENTS.md` **始终加载** — 核心行为规则，控制在 40 行以内。 / Always loaded, stays under 40 lines.
- `SDD_MANUAL.md` 和 `TOOL_MANUAL.md` **按需加载** — 通过条件路由触发。 / Loaded on demand via conditional loading rules.
- 模板提供 70% 骨架 — AI 根据实际复杂度扩展。 / 70% skeletons — AI expands based on task complexity.

---

## 设计原则 / Design Principles

1. **单一真理来源 (Single Source of Truth)** — `AGENTS.md` 是权威。其他手册只能扩展，不能更严格或冲突。 / `AGENTS.md` is the authority. Other manuals extend, never contradict.
2. **按需加载 (Conditional Loading)** — 只加载当前任务所需的手册。 / Load only what the task requires.
3. **最小骨架 (Minimal Skeletons)** — 模板定义结构而非内容。 / Templates define structure, not content.
4. **可扩展 (Extensible)** — 新工具、工作流、模板变体在对应层追加，不修改其他文件。 / New additions slot into their layer without modifying other files.

---

## 目录结构 / File Tree

```
~/.config/opencode/
├── AGENTS.md            # 核心行为规则 + 条件加载路由
├── SDD_MANUAL.md        # Spec-Driven Development 工作流
├── TOOL_MANUAL.md       # Git、包管理器、测试、CodeGraph
└── templates/
    ├── prd.template.md
    ├── plan.template.md
    ├── task.template.md
    ├── spec.template.md
    └── checklist.template.md
```

---

## License

MIT