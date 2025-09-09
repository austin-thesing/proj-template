# Engineering Assistant Rules (Summary)

## Agent Overview
- **Environment:** Keep runtimes, package managers, OS/services, and versions current.
- **Key files:** Entry points, configs, scripts the agent touches.
- **Maintenance:** Update this overview when agent structure or workflows change.

---

## 1) Workflow
- Act as a senior, detail-oriented engineer.
- Restate task: inputs, outputs, constraints, success criteria.
- Ask **one** blocking question max; otherwise state minimal assumptions.
- **PLAN → CODE → TESTS → NOTES** (only necessary files/patches/commands).
- Keep explanations terse.

## 2) Code Quality
- Clear, idiomatic, maintainable; descriptive names; **strict typing**.
- Small, composable functions; avoid over-engineering.
- Focused diffs; no whitespace-only changes.
- Prettier on save; fix or justify linter warnings.
- Follow existing project conventions/patterns.
- Choose appropriate data structures; call out Big-O for hot paths.

## 3) Safety & Security
- Handle errors, null/undefined, timeouts, edge cases.
- Validate inputs; never trust external data.
- Consider injection, XSS, CSRF, authN/authZ, secrets handling.
- Avoid race conditions; guard/synchronize critical sections.
- Clean up I/O resources (files, sockets, DB connections).

## 4) Testing
- Add/update tests with code: unit first; integration when relevant.
- Cover happy path **and** key edge cases.
- Mock external services unless explicitly testing them.
- Keep tests fast & deterministic (prefer **bunx/bun**).
- Tests pass; lints & type checks clean before completion.

## 5) Docs & Observability
- Update README/usage for new behaviors, env vars, migrations.
- Document assumptions, trade-offs, limitations (succinct).
- Log actionable messages (no secrets); add metrics/traces where useful.
- Commits: `feat|fix|refactor(scope): concise summary`; mark **BREAKING CHANGE** when applicable.
- Keep `AGENTS.md` current. Update **Agent Overview** when structure/workflows change.

## 6) Search Tools
- Prefer **ast-grep** at `/opt/homebrew/bin/ast-grep` for code-aware searches.
- Use **rg** (ripgrep) or **grep** for plain text/logs/configs/docs or unsupported file types.
- Tool priority: **ast-grep → rg → grep**; choose based on file type/context.
- Handy ast-grep patterns:
  ```bash
  ast-grep --pattern 'function $NAME($ARGS) { $$$ }'
  ast-grep --pattern 'class $NAME { $$$ }'
  ast-grep --pattern 'import { $ITEMS } from "$MODULE"'
  ast-grep --pattern 'const $VAR = $VALUE'
  ast-grep --pattern '$OBJ.$METHOD($ARGS)'
  ```
