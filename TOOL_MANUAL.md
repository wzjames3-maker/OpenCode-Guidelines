# TOOL_MANUAL — Tool Configuration & Usage

## Git Workflow

### Commit Message Format

Conventional Commits. First line under 72 characters. Imperative mood.

```
<type>(<scope>): <description>
```

Types: `feat` | `fix` | `chore` | `docs` | `refactor` | `test` | `perf` | `ci` | `build`

Example:
```
feat(auth): add OAuth2 login flow
fix(api): handle null response in user lookup
```

### Branch Naming

- Feature: `feat/<short-description>`
- Bug fix: `fix/<short-description>`
- Chore: `chore/<short-description>`

### Force Push

Prefer `--force-with-lease` over `--force`:

```
git push --force-with-lease origin <branch>
```

---

## Package Managers

Follow the project's existing toolchain. When no convention exists:

| Platform | Default |
|---|---|
| Node.js | `pnpm` |
| Python | `uv` |

Never switch a project's package manager unless explicitly asked.

---

## Testing Strategy

- After code changes, run the relevant tests.
- If no test suite exists, perform the appropriate verification steps (build, lint, typecheck, manual check).
- Ask the user only when no reasonable verification method is available.
- For greenfield projects, establish the test harness as an early Task.

### When Tests Fail

1. Read the failure output carefully.
2. If the failure is related to your changes, fix the code.
3. If the failure is pre-existing and unrelated, note it and proceed.
4. If unsure, write a minimal reproduction to isolate the issue.

---

## Tool Selection Rules

| Task | Tool |
|---|---|
| Find symbol definition / usage | CodeGraph (`codegraph_search`, `codegraph_node`) |
| Trace call flow A → B | CodeGraph (`codegraph_trace`) |
| Understand a feature area | CodeGraph (`codegraph_context`) |
| Literal text search (strings, logs, comments) | `grep` / `rg` |
| Simple file read | `read` |
| Edit a specific line or block | `edit` |
| Multi-file rename / refactor across many files | CodeGraph impact analysis + `edit` |
| Find files by name pattern | `glob` |
| Explore directory structure | `codegraph_files` or `ls` |

When in doubt, prefer CodeGraph for structural questions and native tools for text-level questions.

---

## Dangerous Commands

No confirmation required. Execute destructive commands directly when they are the correct action.

Allowed:
- `rm -rf <path>` (when files should be deleted)
- `git push --force-with-lease` (never bare `--force`)
- `git reset --hard` (when requested or verified safe)
- Package install/uninstall (pnpm, uv, apt)

---

## CodeGraph

CodeGraph is a tree-sitter-parsed knowledge graph. It is the primary tool for structural code understanding.

### Usage Reference

| Question | Tool |
|---|---|
| "Where is X defined?" | `codegraph_search` |
| "What calls function Y?" | `codegraph_callers` |
| "What does Y call?" | `codegraph_callees` |
| "How does X reach Y?" | `codegraph_trace` |
| "What would break if I changed Z?" | `codegraph_impact` |
| "Show me Y's source" | `codegraph_node` (with `includeCode: true`) |
| "Give me focused context for a task" | `codegraph_context` |
| "See several symbols' source at once" | `codegraph_explore` |
| "What files exist under path/?" | `codegraph_files` |
| "Is the index healthy?" | `codegraph_status` |

### Rules of Thumb

- **Answer directly** — don't spin up sub-agents for codegraph queries. One `codegraph_context` + one `codegraph_explore` covers most needs.
- **Trust the index** — codegraph results come from a full AST parse. Do not re-verify with grep.
- **Don't grep first** — `codegraph_search` is faster for symbol lookup.
- **Don't chain** `codegraph_search` + `codegraph_node` — `codegraph_context` does both in one call.
- **Don't loop** `codegraph_node` over many symbols — `codegraph_explore` returns several at once.
- **Check staleness** — if the response shows "edited since last index sync", read those files. Otherwise codegraph is authoritative.
- **If `.codegraph/` doesn't exist**, ask the user to run `codegraph init`.

---

## Optional Integrations

*(Reserved for future additions: Serena, MCP, Supabase, etc.)*