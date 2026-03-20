---
name: commit
description: >-
  Creates git commits in this repository using a fixed conventional message
  shape. Use when the user asks to commit, save work to git, stage changes, or
  record a snapshot; also when finishing a task that should be persisted with
  version control.
---

# Commit

## Message format (required)

Single-line subject (no trailing period):

```text
<type>(<scope>): <Imperative description with lowercase after the colon>
```

**Example (canonical for this repo):**

```text
feat(dn): Add new diagram for candidates component
```

- **type:** `feat` | `fix` | `docs` | `chore` | `refactor` | `style` | `test` — pick the closest [Conventional Commits](https://www.conventionalcommits.org/) type.
- **scope:** Short **lowercase** area tag. Prefer the table below; if nothing fits, use a new 2–4 letter token aligned to the change.
- **description:** Imperative mood, concise; **first word after `:` is capitalized** to match the project example; no period at end.

### Suggested scopes (LTI design repo)

| scope | Use for |
|-------|--------|
| `dn` | Diagrams (Lean Canvas, use case, C4, HLD, etc.) |
| `doc` | Main deliverable markdown (`LTI-*.md`) narrative/structure |
| `prompts` | `prompts.md` or prompt log |
| `rules` | `.cursor/rules` |
| `skills` | `.cursor/skills` |
| `repo` | Root README, shared repo layout, `.gitignore`, CI |

For multiple unrelated changes, **prefer separate commits**; do not mix scopes in one vague message.

## Workflow

1. Run `git status` (and `git diff` / `git diff --staged` if needed) so the commit matches what changed.
2. Stage **only** paths the user intends: `git add <paths>`. Avoid `git add -A` unless the user asked to commit everything.
3. Compose the subject line; **must** match the format above. Add a body after a blank line only if the change needs context (breaking change, rationale, links).
4. Commit with `git commit -m "type(scope): Subject"` (and second `-m` for body if used). Request **git_write** permission when executing.

## Guardrails

- Do not commit secrets, API keys, or large accidental files; if present, stop and surface the issue.
- If there is nothing to commit, say so instead of an empty commit.

## Examples

See [examples.md](examples.md) for more message samples.
