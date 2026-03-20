---
name: improve-story
description: >-
  Refines a story into an actionable task spec at ai-specs/tasks/<NNN>-task.md
  with clear acceptance criteria. Use when the user needs execution-ready tasks,
  not phased roadmaps (use plan-story for those).
---

# Improve story → task spec

## Purpose

Rewrite informal input into a **structured task specification** engineers can execute **without guesswork**, stored under **`ai-specs/tasks/<NNN>-task.md`**.

## When to Use

- The user pastes or points to a **story** and wants **clearer scope** and **acceptance criteria**.
- They need **Given/When/Then**-style checks or **edge cases** before design/implementation.

## When Not to Use

- The user wants **phased delivery planning** without full AC → **plan-story** (`ai-specs/plan/<NNN>-plan.md`).
- The user wants a **PRD** or product-wide requirements → **generate-prd**.
- The user wants a **cross-doc audit** → **validate-artifacts**.

## Inputs

- **Story**: text, bullets, ticket paste, or path to a file (do not overwrite source unless asked).

## Outputs

- Markdown file at:

```text
ai-specs/tasks/<NNN>-task.md
```

- **`<NNN>`** — three-digit zero-padded: `001`, `002`, …
- **Next `<NNN>` for a new file:** list `ai-specs/tasks/` for **`^\d{3}-task\.md$`**, **max + 1**, or **`001`** if missing/empty.
- Create **`ai-specs/tasks/`** and **`ai-specs/`** if absent.

**Forbidden ambiguous form:** path ending in only `-task.md` without a numeric prefix.

## Process

1. Parse the story; **one** minimal clarification only if **blocking**; else use **Open questions**.
2. Resolve path per **Create vs Update Guidance**.
3. Fill **Output file template**; preserve ticket IDs / feature flags from input.
4. Report the **exact path** to the user.

## What “improve” means

1. **Title** — Outcome-oriented (**H1**).  
2. **Context** — Why now, who benefits, links to product/architecture if known.  
3. **User story** — *As a … I want … so that …* when it fits (adapt for technical work).  
4. **Scope** — **In scope** / **Out of scope** bullets.  
5. **Acceptance criteria** — Numbered, **testable**; **Given / When / Then** where it helps.  
6. **Edge cases & errors** — Permissions, failures, idempotency if relevant.  
7. **Dependencies** — Tasks, APIs, data, flags.  
8. **Open questions** — Unknowns; **do not invent facts**.  
9. **Non-goals / notes** — Optional.

## Output file template

Use this shape in **`ai-specs/tasks/<NNN>-task.md`** (adapt if purely technical):

```markdown
# <Improved title>

## Context

## User story

## Scope
- **In scope:**
- **Out of scope:**

## Acceptance criteria
1. …

## Edge cases and errors

## Dependencies

## Open questions

## Source
<!-- Brief note: pasted story / file path / chat reference; omit secrets -->
```

## Quality Checks

| Check | Pass |
|-------|------|
| Path | Exactly `ai-specs/tasks/<NNN>-task.md` with three-digit `NNN` |
| Acceptance criteria | Each item is **verifiable** (observable outcome or test), not vague “handle well” |
| Scope | **Out of scope** present when ambiguity is likely |
| Numbering | New file uses **next** free `NNN`; edits retain same `NNN` |

**Bad output:** Restated vague goals without AC, missing **Open questions** when inputs were thin, duplicate **H1** sections.

**Good output:** Numbered AC, explicit edges, traceable **Source**, path confirmed.

## Create vs Update Guidance

| Situation | Action |
|-----------|--------|
| **New** task file (default) | Next free `<NNN>`; write **`ai-specs/tasks/<NNN>-task.md`**. |
| **Revise** existing `ai-specs/tasks/<NNN>-task.md` | **Edit in place**; keep the same `<NNN>`; update **H1**/sections; append to **Open questions** rather than deleting tracked items unless user asked. |
| User asked for “another version” | Use **new** `<NNN>`; in **Source**, cite prior file path. |
| Collision risk | If two tasks would share the same title and `NNN` is unclear, **list** existing `*-task.md` files and pick next `NNN`; do not overwrite. |

**Overwrite rule:** Do not replace an existing `<NNN>-task.md` with unrelated content without explicit user confirmation.

## Common Mistakes to Avoid

- Creating a **plan** in `ai-specs/tasks/` (wrong skill/folder pattern).
- Inventing **API contracts** or **SLAs** not stated by the user—flag as **Open questions** instead.
- Secrets in **Source** or body—**redact**.
