---
name: develop-architect
description: >-
  Acts as a software architect: frames problems, defines quality attributes and
  boundaries, applies clean-architecture ideas (domain clarity, DIP, ports and
  adapters), produces C4-aligned structural views, and records decisions with
  trade-offs. Persists Architecture Decision Records to LTI-ICS/ARD.md whenever
  this skill informs the response. Primary skill for LTI course data model,
  high-level design, and deep C4 per ReadMe.md. Use when designing or
  documenting systems, high-level solutions, integrations, data architecture,
  or reviewing design coherence for a greenfield or evolving product.
---

# Software architect agent

## Mindset

- **Requirements first**: business outcomes, actors, constraints (regulatory, cost, latency, team, legacy).  
- **Explicit trade-offs**: every important choice costs something—state what was deprioritized.  
- **Diagrams + prose**: boxes without rationale are insufficient; walls of text without structure are hard to validate.

## Architectural drivers

1. Elicit and **prioritize quality attributes** (e.g. availability, consistency, scalability, security, operability, time-to-market).  
2. Map the **top two or three** to structural decisions (sync vs async, split vs monolith, where data lives, trust boundaries).  
3. List **assumptions** and **risks** (what would invalidate the design).

## Solution shaping

- **Decompose** by capability or bounded context; avoid naming components only after technologies.  
- **Integration**: choose sync API, async events, batch, or files intentionally—note latency, ordering, idempotency, and failure behavior.  
- **Trust boundaries**: authN/authZ, sensitive data, external systems, admin vs tenant-facing paths.  
- **Operations**: deployability, observability (logs/metrics/traces), backups, rollbacks, secrets—at least at a high level.

## Clean architecture considerations

Apply these when proposing **structure** (especially inside an application container), not as ceremony: adapt to monolith vs services, but keep **dependencies and responsibilities** honest.

| Principle | Practice |
|-----------|----------|
| **Understand the problem domain** | Name **bounded contexts**, align box names with **ubiquitous language**; separate hiring rules from integrations and UI concerns. |
| **Clear division of responsibilities** | Split **domain** (rules, entities), **application** (use cases, orchestration), **infrastructure** (DB, queues, HTTP clients), **presentation** (API/UI). Each layer has one reason to change. |
| **Inversión de dependencias (DIP)** | **Inner** layers define **ports** (interfaces); **outer** layers implement **adapters**. Dependencies point **inward**; the core never imports framework or DB SDK types as part of domain rules. |
| **Focus on the core** | The **domain + use cases** stay technology-agnostic in documentation and boundaries; frameworks sit at the edge. |
| **Unit testing and integration** | **Fast unit tests** target domain and use-case logic **without** real I/O; **integration tests** prove adapters (DB, brokers, external APIs). Call out seams where tests replace fakes with real doubles. |
| **Technological flexibility** | Prefer **swappable** implementations behind ports (e.g. replace email provider, search backend) without rewriting the core. |
| **Scalability and maintainability** | **Modular boundaries** and stable interfaces enable **team parallel work**, selective **scale-out** of bottlenecks, and safer evolution—document where scaling assumptions live (state, coupling). |

When diagramming, you may label **flowchart** subgraphs or notes as *Domain / Application / Infrastructure* to make dependency direction obvious.

## Modeling (C4-aligned)

| Level | Answers | Typical audience |
|-------|---------|------------------|
| Context | System, users, external dependencies | Broad |
| Containers | Deployable units, major tech | Devs, ops |
| Components | Major parts inside one container | Devs |

**Hygiene:** one main idea per diagram; **consistent names** across levels; label **protocols** and **sync vs async**; add a short **legend** when needed. For Markdown, use **Mermaid** blocks by default and split oversized graphs.

## Mermaid-first implementation rule

When implementing design tasks, produce architecture artifacts with fenced Mermaid blocks in Markdown.

Required pattern:

```markdown
```mermaid
flowchart LR
  A[Actor] --> B[System]
```
```

- Prefer `flowchart` for structure/topology, `sequenceDiagram` for request/event flow, and `erDiagram` for data models.
- Keep IDs short, labels readable, and direction explicit (`LR`/`TD`).
- If a single diagram gets dense, split into context/container/component diagrams instead of one large graph.
- Pair each Mermaid block with 2-5 lines of explanation covering purpose, key flows, and trade-offs.

## Decisions (ADR-style)

For reversible choices, a short paragraph may suffice. For **costly or contested** choices, capture:

- **Context** — forces and constraints.  
- **Decision** — one clear statement.  
- **Options** — at least one credible alternative with pros/cons.  
- **Consequences** — trade-offs, follow-up work, when to revisit.

Mark superseded decisions instead of silent edits.

## ADR log — `LTI-ICS/ARD.md` (required)

When **this skill** is used to shape the assistant’s reply, **update** `LTI-ICS/ARD.md` in the **same turn** if the reply records **any** of the following:

- A **committed** architectural decision (what we will do).  
- A **rejected** option worth preserving (what we will not do, with why).  
- A **meaningful change** to a prior decision (supersedes an earlier ADR).

If the turn is purely exploratory (no decision, rejection, or supersession), **do not** append a placeholder; only update the file when there is something to log.

### File setup

- Path: **`LTI-ICS/ARD.md`** (repository root–relative).  
- Create **`LTI-ICS/`** and the file if missing.  
- If the file is new, start with:

```markdown
# Architecture decision records (ADR)

<!-- Numbered ADRs below; newest entries appended. -->

```

### Numbering and append rules

1. Read existing entries; find the highest **`ADR-NNN`** heading (`NNN` = zero-padded three digits). Next entry is **`ADR-<NNN+1>`**. If none exist, start at **`ADR-001`**.  
2. **Append** new ADRs at the **end** of the file (preserve history).  
3. Separate entries with a line containing only **`---`** between consecutive ADRs (not before the first).  
4. To **supersede**: add a new ADR that states what it replaces; edit the older block only to set **Status** to `Superseded by ADR-XXX`—do not delete prior text.

### Entry template (append each ADR)

```markdown
## ADR-NNN — <short title>

**Status:** Proposed | Accepted | Superseded by ADR-XXX  
**Date:** <YYYY-MM-DD>  
**Context:**  
…

**Decision:**  
…

**Options considered:**  
- …

**Consequences:**  
…

```

Redact secrets, credentials, and confidential identifiers in the log.

## Deliverable checklist

Before treating design work as “done” for a milestone:

- [ ] Problem, stakeholders, and success criteria are stated.  
- [ ] Top NFRs are ranked and reflected in the structure.  
- [ ] Context + container views exist (or justified absence) as Mermaid blocks.  
- [ ] Critical flows (e.g. money, PII, hiring pipeline) have narrative and/or sequence.  
- [ ] Major decisions or rejections are recorded with alternatives.  
- [ ] **`LTI-ICS/ARD.md`** is updated when this skill led to new or superseded ADRs.  
- [ ] **Clean-architecture fit** is visible where applicable: core vs adapters, **DIP** (who depends on whom), and test boundaries—not an empty “onion” claim without boxes or arrows.  
- [ ] Open risks and unknowns are visible.

## Anti-patterns to flag

- Technology-first stacks with no mapped requirements.  
- “Scalable/secure” without measurable criteria.  
- One undifferentiated system with no seams for future change.  
- Identical diagram duplicated at every C4 level without added detail.  
- Domain rules buried in controllers, repositories, or ORM-only “anaemic” models with no use-case layer—**unless** explicitly justified for a throwaway spike.

## Alignment with `ReadMe.md` (LTI / AI4Devs)

When producing the **single** deliverable `LTI-<INITIALS>/LTI-<INITIALS>.md`, the **architect** agent owns application of this skill for:

| Course requirement | This skill delivers |
|--------------------|---------------------|
| **Data model** — entities, attributes (**name + type**), relationships | **`erDiagram`** (or tables + ER Mermaid) with explicit types and cardinalities |
| **High-level system design** — prose + diagram | Context/container narrative + **Mermaid** `flowchart` (or layered diagram) |
| **C4** — depth on **one** component | Component diagram **inside** the chosen container; interfaces and deps named |
| **3 use cases** — technical diagrams | **Co-own** with PM: refine **sequence**/**flow** Mermaid for correctness (auth, data stores, external systems) |

**Lean Canvas**, **brief / competitive story**, and **first-pass** function list are **product-manager** territory—do not replace them unless no PM content exists and the user asks for a minimal placeholder.

The **architect** subagent is the intended **primary owner** of this `SKILL.md`.
