---
name: plan-story
description: >-
  Turns a user-supplied story into an execution plan (phases, work items,
  risks, dependencies) and saves it under ai-specs/plan as a numbered plan
  file. Use when the user wants a roadmap, breakdown, or delivery plan from an
  idea, ticket, or brief without yet refining full acceptance criteria.
---

# Plan story → plan spec

## Trigger

The user provides a **story** (text, draft, ticket paste, or path to a file). **Do not** overwrite their source unless they ask; **always** write the plan to **`ai-specs/plan/`** as below.

## Output path (required)

```
ai-specs/plan/<NNN>-plan.md
```

- **`NNN`** is a **three-digit zero-padded** sequence: `001`, `002`, …  
- **Next number:** list `ai-specs/plan/` for files matching `^\d{3}-plan\.md$`, take the **highest** `NNN`, add **1**. If the directory is missing or empty, use **`001`**.  
- Create `ai-specs/plan/` (and `ai-specs/`) if they do not exist.

## What “plan” means

Produce a **delivery-oriented plan** the team can follow or slice further:

1. **Goal & outcome** — What “done” means for this story in one short paragraph.  
2. **Assumptions** — Only what the plan relies on; separate from **Open questions**.  
3. **Constraints** — Time, tech, policy, or coupling called out by the user or clearly implied.  
4. **Work breakdown** — Numbered phases or work packages; each item has a clear deliverable. Prefer dependency order (foundation → integration → polish).  
5. **Milestones / checkpoints** — Optional but useful for multi-step work (demo points, design freeze, release gate).  
6. **Dependencies** — People, systems, data, prior tasks, feature flags.  
7. **Risks & mitigations** — Top 3–5; include **spikes** or proof-of-concept steps if uncertainty is high.  
8. **Definition of ready (for build)** — Short list of what must be true before heavy implementation (e.g. API contract, UX signoff).  
9. **Open questions** — Unknowns that affect scope or order; do not invent facts.

If the story is tiny, keep the plan short; avoid ceremony for its own sake.

## Output file template

```markdown
# <Plan title>

## Goal and outcome

## Assumptions

## Constraints

## Work breakdown
1. …
2. …

## Milestones

## Dependencies

## Risks and mitigations

## Definition of ready (for build)

## Open questions

## Source
<!-- Brief note: pasted story / file path / chat reference; omit secrets -->
```

## Workflow

1. Parse the given story; ask **one** minimal clarification only if blocking (otherwise use **Open questions**).  
2. Compute **NNN** and write `ai-specs/plan/<NNN>-plan.md` with the plan.  
3. Tell the user the **exact path** created.

## Guardrails

- No secrets or confidential data in **Source** or body; redact if the input contained any.  
- Do not bump the sequence when **editing** an existing `<NNN>-plan.md`; for a **new** plan file, always use the **next** free `NNN`.  
- A **plan** file is not a full task spec: it may reference follow-up work (e.g. run **improve-story** per slice) if that keeps the plan lean.
