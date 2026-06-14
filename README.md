# OpenCode Guidelines

一套为 [opencode](https://opencode.ai) 设计的四层 Agent OS 配置，面向 Spec-Driven Development 和结构化工具使用。

## 架构

| 层 | 文件 | 职责 |
|---|---|---|
| **行为层 (Behavior)** | `AGENTS.md` | 沟通规范、核心原则、条件加载路由 |
| **工作流层 (Workflow)** | `SDD_MANUAL.md` | Spec-Driven Development 全流程与工件管理 |
| **能力层 (Capability)** | `TOOL_MANUAL.md` | Git 工作流、包管理器、测试策略、工具选型、CodeGraph 使用 |
| **产出层 (Artifact)** | `templates/*.template.md` | PRD / Plan / Task / Spec / Checklist 最小骨架 |

## 使用方式

复制到 `~/.config/opencode/`：

```bash
cp -r ./* ~/.config/opencode/
```

也可按需选取单个文件。

### 如何工作

- `AGENTS.md` **始终加载** — 核心行为规则，控制在 40 行以内。
- `SDD_MANUAL.md` 和 `TOOL_MANUAL.md` **按需加载** — 通过 `AGENTS.md` 中的条件路由规则触发。
- 模板提供 70% 骨架 — AI 根据实际任务复杂度自行扩展，不填充空标题。

## 设计原则

1. **单一真理来源 (Single Source of Truth)** — `AGENTS.md` 是权威。Workflow 和 Capability 文件只能扩展细节，不能比 AGENTS 更严格，也不能与之冲突。
2. **按需加载 (Conditional Loading)** — 避免上下文污染。只加载当前任务所需的手册。
3. **最小骨架 (Minimal Skeletons)** — 模板定义结构而非内容。不预设任何具体描述。
4. **可扩展 (Extensible)** — 新工具、新工作流或新模板变体只需在对应层追加，无需修改其他文件。

## 目录结构

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

## License

MIT