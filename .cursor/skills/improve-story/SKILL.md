---
name: improve-story
description: >-
  Refines a user-supplied story into a clearer, actionable specification and
  writes it under ai-specs/tasks as a numbered task file. Use when the user
  pastes or points to a story to improve, sharpen acceptance criteria, or turn
  informal notes into a structured task for implementation or design.
---

# Improve story → task spec

## Trigger

The user provides a **story** (text, bullet draft, ticket paste, or path to a file). **Do not** overwrite their source unless they ask; **always** emit the improved version to **`ai-specs/tasks/`** as specified below.

## Output path (required)

```
ai-specs/tasks/<NNN>-task.md
```

- **`NNN`** is a **three-digit zero-padded** sequence: `001`, `002`, …  
- **Determine the next number:** list `ai-specs/tasks/` for files matching `^\d{3}-task\.md$`, take the **highest** `NNN`, add **1**. If the directory is missing or empty, use **`001`**.  
- Create `ai-specs/tasks/` (and `ai-specs/`) if they do not exist.

## What “improve” means

Rewrite and structure so engineers can execute without guesswork:

1. **Title** — Short, outcome-oriented (update H1 in the file).  
2. **Context** — Why now, who benefits, links to product/architecture if known.  
3. **User story** — Classic form when it fits: *As a … I want … so that …* (adjust if non-user work).  
4. **Scope** — In scope / **Out of scope** bullets.  
5. **Acceptance criteria** — Numbered, testable checks; prefer **Given / When / Then** where it clarifies behavior.  
6. **Edge cases & errors** — Empty states, permissions, failures, idempotency if relevant.  
7. **Dependencies** — Other tasks, APIs, data, flags.  
8. **Open questions** — Explicit unknowns; do not invent facts.  
9. **Non-goals / notes** — Optional; keep assumptions visible.

Preserve identifiers (ticket IDs, feature flags) if the user supplied them.

## Output file template

Use this shape in `<NNN>-task.md` (adapt sections if the story is technical with no end-user):

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

## Workflow

1. Parse the given story; ask **one** minimal clarification only if blocking (otherwise use **Open questions**).  
2. Compute **NNN** and write `ai-specs/tasks/<NNN>-task.md` with improved content.  
3. Tell the user the **exact path** created.

## Guardrails

- No secrets or confidential data in **Source** or body; redact if the input contained any.  
- Do not bump the sequence for edits to an **existing** `<NNN>-task.md` unless the user asked to add a **new** file; then still use the **next** free `NNN`.
