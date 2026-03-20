---
name: generate-prd
description: >-
  Produces a Product Requirements Document (PRD) for an Applicant Tracking
  System from a short general description. Use when the user asks for a PRD,
  product spec, requirements doc, roadmap inputs, or LTI/ATS scope from a brief.
---

# Generate PRD (ATS)

## Trigger

The user supplies a **general description** of an **Applicant Tracking System** (vision, problem, audience, or bullet notes). Expand it into a structured **PRD** in Markdown. Do not invent compliance claims or integrations; capture unknowns under **Open questions**.

## Output path (default)

```
ai-specs/prd/<NNN>-prd.md
```

- **`NNN`**: three-digit zero-padded sequence (`001`, `002`, …). Scan `ai-specs/prd/` for `^\d{3}-prd\.md$`, use **max + 1**, or **`001`** if missing/empty. Create directories if needed.  
- If the user names a different path, use that instead and skip sequencing.

## ATS domain lenses (use where relevant)

- **Entities:** requisitions/jobs, candidates/applications, pipeline stages, offers, users/roles (recruiter, hiring manager, admin).  
- **Flows:** sourcing, apply, screen, interview schedule, feedback, decision, hire/reject, compliance/consent.  
- **Collaboration:** real-time or shared visibility between recruiters and hiring managers.  
- **Automations & AI:** scoring, scheduling assistance, drafting, **human-in-the-loop** where decisions affect candidates.  
- **Non-functional:** privacy, retention, audit trails, accessibility, performance, integrations (HRIS, calendar, email).

## PRD template (required sections)

Use this outline; adapt depth to the input size.

```markdown
# <Product name> — Product Requirements Document

## Document control
- **Version:** 0.1
- **Last updated:** <YYYY-MM-DD>
- **Author / source:** <brief note>

## Executive summary
<!-- Problem, opportunity, and recommended direction in ~5–10 sentences. -->

## Goals and non-goals
### Goals
### Non-goals

## Target users and personas
<!-- Recruiter, hiring manager, candidate (if in-scope), admin — goals and pains. -->

## Problem statement
## Proposed solution (high level)

## User journeys (summary)
<!-- 2–5 bullets per primary journey; link to future use-case docs if needed. -->

## Functional requirements
<!-- Numbered FRs: FR-001 … Each testable; mark MoSCoW or Priority P0–P3 if helpful. -->

## Non-functional requirements
<!-- NFR categories: security, privacy, performance, reliability, accessibility, observability. -->

## Success metrics
<!-- Leading/lagging metrics; avoid vanity metrics. -->

## Milestones / phasing
<!-- MVP vs later; dependencies called out. -->

## Risks, assumptions, dependencies

## Open questions
<!-- Explicit gaps; do not fabricate vendor or legal detail. -->

## Appendix
### Glossary
### References
```

## Quality bar

- **Testable FRs** — “The system shall …” / clear acceptance per item.  
- **Traceability** — goals → FRs → metrics where obvious.  
- **Tone** — product-level; defer **component-level C4** and **typed ERD** depth to **develop-architect** / architect agent (see below).  
- **Secrets** — redact if the paste contains tokens, salaries, or PII.

## Alignment with `ReadMe.md` (LTI / AI4Devs deliverable)

When the PRD supports the **course bundle** (single `LTI-<INITIALS>/LTI-<INITIALS>.md`), ensure the PRD (or a summarized export into that file) can supply:

| Course checklist item | In PRD (this skill) |
|----------------------|---------------------|
| Brief description, value, competitive advantages | **Executive summary**, **Goals**, **Proposed solution** |
| Main functions | **Functional requirements**, **User journeys** |
| Lean Canvas | Add section **## Lean Canvas** with a **Mermaid** diagram or equivalent structure (problem, solution, metrics, unfair advantage, channels, segments, cost, revenue) |
| 3 main use cases + diagram each | Add **## Use cases** with exactly **three** `###` subsections; each: short narrative + fenced **`mermaid`** (`sequenceDiagram` or `flowchart`) |
| Data model (entities, attributes+types, relationships) | Add **## Data model (conceptual)** listing entities and relationships; **types** may be preliminary—flag “finalize with architect” if full precision is required |
| High-level system design + diagram | Add **## High-level system design** with prose + one **Mermaid** context/container-style diagram at product-appropriate depth |
| C4 depth on one component | Add **## C4 component focus (draft)** with Mermaid if possible, or a bullet handoff: “Detailed C4: use **develop-architect** / `/architect`” |

The **product-manager** agent is the intended **primary consumer** of this skill; PRD output can live in `ai-specs/prd/<NNN>-prd.md` **and** be **merged** into the student’s `LTI-*` main doc for accuracy against `ReadMe.md`.

## Workflow

1. Parse the user’s ATS description; one clarifying question only if blocking.  
2. Write the PRD using the template; default save to `ai-specs/prd/<NNN>-prd.md`.  
3. Reply with the **exact path** and a one-paragraph summary of scope.
