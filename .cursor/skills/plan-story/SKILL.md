---
name: plan-story
description: >-
  Turns a user story or brief into a numbered execution plan under
  ai-specs/plan/<NNN>-plan.md. Use for roadmaps and phased breakdowns without
  full acceptance criteria. Does not replace improve-story task specs.
---

# Plan story → plan spec

## Purpose

Produce a **delivery-oriented plan** (phases, dependencies, risks) saved as a **new numbered file** under `ai-specs/plan/`, without overwriting the user’s source material.

## When to Use

- The user wants a **roadmap**, **breakdown**, or **delivery plan** from an idea, ticket, or brief.
- They need **sequencing** and **dependencies** more than **Given/When/Then** acceptance (use **improve-story** for the latter).

## When Not to Use

- The user needs **testable acceptance criteria** as the main output → use **improve-story** (`ai-specs/tasks/<NNN>-task.md`).
- The user only wants **product goals / FRs** → use **generate-prd**.
- The user asked for a **validation pass** only → use **validate-artifacts**.

## Inputs

- A **story**: pasted text, ticket body, or path to a file.
- Optional: **existing plan path** to revise (then follow **Create vs Update**).

## Outputs

- **New or updated** Markdown file at:

```text
ai-specs/plan/<NNN>-plan.md
```

- **`<NNN>`** — three-digit zero-padded integer: `001`, `002`, …
- **Next `<NNN>` for a new file:** list `ai-specs/plan/` for files matching **`^\d{3}-plan\.md$`**, take the **highest** `NNN`, add **1**; if directory missing or empty → **`001`**.
- Create **`ai-specs/plan/`** and **`ai-specs/`** if absent.

**Forbidden ambiguous form:** a path ending in only `-plan.md` without a numeric prefix.

## Process

1. Parse the story; **one** minimal clarification only if **blocking**; otherwise capture unknowns under **Open questions**.
2. Resolve target path per **Create vs Update Guidance**.
3. Write the plan using **Output file template** below.
4. Tell the user the **exact path** written.

## What “plan” means

1. **Goal & outcome** — What “done” means in one short paragraph.  
2. **Assumptions** — Only what the plan relies on; separate from **Open questions**.  
3. **Constraints** — Time, tech, policy, or coupling from user or clear implication.  
4. **Work breakdown** — Numbered phases or packages; dependency order (foundation → integration → polish).  
5. **Milestones / checkpoints** — Optional; demos, design freeze, release gate.  
6. **Dependencies** — People, systems, data, prior tasks, flags.  
7. **Risks & mitigations** — Top 3–5; include **spikes** if uncertainty is high.  
8. **Definition of ready (for build)** — What must be true before heavy implementation.  
9. **Open questions** — Unknowns affecting scope/order; **do not invent facts**.

If the story is tiny, keep the plan short.

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

## Quality Checks

| Check | Pass |
|-------|------|
| File path | Matches `ai-specs/plan/<NNN>-plan.md` with three-digit `NNN` |
| New file numbering | Uses **next** free `NNN`, not a duplicate number for a **different** plan |
| Content | All template sections present or explicitly marked N/A (only for Milestones if unused) |
| Safety | Source story path or paste **not** deleted or overwritten unless user asked |

**Bad output:** Vague phases with no deliverables, invented dates/facts, or wrong `NNN` colliding with an existing plan.

**Good output:** Ordered work, explicit risks and open questions, correct path echoed to the user.

## Create vs Update Guidance

| Situation | Action |
|-----------|--------|
| **New** plan (default) | Compute **next** `<NNN>`; **create** `ai-specs/plan/<NNN>-plan.md`. |
| **Revise** existing `ai-specs/plan/<NNN>-plan.md` | **Edit that file only**; **do not** change `<NNN>`; **do not** create a second file unless the user wants a **forked** plan (then use **next** `<NNN>` and reference the prior file in **Source**). |
| User did not specify which plan to update | **Read** `ai-specs/plan/`; if ambiguous, ask **one** question or default to **new** `<NNN>` and note the assumption in **Source**. |
| Duplicate sections | **Merge** into a single section per heading; remove duplicate **H1**s. |

**Overwrite rule:** Never replace an existing `<NNN>-plan.md` with unrelated content without user confirmation.

## Common Mistakes to Avoid

- Bumping `<NNN>` when **editing** an existing plan file.
- Using **improve-story** task template for a **plan** (wrong artifact).
- Putting secrets in **Source** or body—**redact**.
