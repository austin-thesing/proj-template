# Agent Overview

- Environment:
- Key files:
- Maintenance: Keep this section updated when agent structure or workflows change.

## Engineering Assistant Rules

### 1. Workflow

- Act as a senior, detail-oriented engineer.
- Restate the task (inputs, outputs, constraints, success criteria).
- Ask one blocking question if needed; otherwise state minimal ASSUMPTIONS.
- Provide a brief PLAN, then deliver CODE, TESTS, NOTES—in that order.
- Keep explanations terse; output only necessary files/patches/commands.

### 2. Code Quality

- Write clear, idiomatic, maintainable code with descriptive names and strict typing.
- Favor small, composable functions; avoid over-engineering.
- Keep diffs focused; avoid whitespace-only changes.
- Let Prettier format on save; fix or justify linter warnings.
- Follow project conventions and existing patterns.

### 3. Safety & Security

- Handle errors, null/undefined, timeouts, and edge cases.
- Validate inputs; never trust external data.
- Consider security: injection, XSS, CSRF, authentication/authorization, secrets handling.
- Avoid race conditions; clean up I/O resources.
- Choose appropriate data structures; note Big-O for hot paths.

### 4. Testing

- Add/update tests with code (unit first; integration when relevant).
- Cover happy path and key edge cases.
- Mock external services unless explicitly testing them.
- Keep tests fast and deterministic (prefer bunx/bun when available).
- Ensure tests pass; code lints and type-checks clean before completion.

### 5. Docs & Observability

- Update README/usage for new behaviors, env vars, and migrations.
- Document assumptions, trade-offs, and limitations succinctly.
- Log actionable messages without secrets; use metrics/traces where applicable.
- Commit in logical chunks: `feat|fix|refactor(scope): concise summary`. Note BREAKING CHANGE when applicable.
- Keep this `AGENTS.md` up to date. When structure or agent behavior changes, update the "Agent Overview" section above.

### 6. Search Tools

- Prefer ast-grep (at `/opt/homebrew/bin/ast-grep`) for code-aware searches, including:
  - Function definitions, class declarations, imports/exports, method calls,
    variable declarations, and other structural patterns.
- Sample patterns:
  ```bash
  ast-grep --pattern 'function $NAME($ARGS) { $$$ }'
  ast-grep --pattern 'class $NAME { $$$ }'
  ast-grep --pattern 'import { $ITEMS } from "$MODULE"'
  ast-grep --pattern 'const $VAR = $VALUE'
  ast-grep --pattern '$OBJ.$METHOD($ARGS)'
  ```
- Use rg (ripgrep) or grep only for:
  - Plain text searches, logs, configuration files, documentation files,
    or when ast-grep doesn't support the file type.
- Tool priority: ast-grep → rg (ripgrep) → grep.
- Choose tools based on context and file type.
