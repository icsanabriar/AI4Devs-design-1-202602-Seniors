# Cursor setup — operational guide

This folder configures **Cursor** for the LTI / AI4Devs design exercise: **agents** (specialized subagents), **skills** (repeatable procedures), and **rules** (governance). The goal is consistent, auditable documentation—not application code.

## Repository map

| Path | Contents |
|------|----------|
| [`.cursor/agents/`](agents/) | Agent definitions: `architect.md`, `product-manager.md`, `documentation-auditor.md` |
| [`.cursor/skills/`](skills/) | One `SKILL.md` per skill (subfolders: `develop-architect`, `generate-prd`, `plan-story`, `improve-story`, `validate-artifacts`, `commit`) |
| [`.cursor/rules/`](rules/) | Numbered `.mdc` rules (`10-` … `60-`), some `alwaysApply`, some scoped by glob |

## Architecture: how the pieces fit

```text
Rules (10–60)     →  MUST / MUST NOT governance; always win on conflict
       ↓
Agents            →  Role boundaries, handoffs, which skills to read first
       ↓
Skills            →  Concrete paths, templates, create/update vs validate
       ↓
Artifacts         →  LTI-* deliverables, ai-specs/*, prompts.md, ARD.md
```

- **Rules** apply to any assistant turn when in scope (`alwaysApply` or matching glob). They define course layout, prompt logging, paths, diagrams, validation expectations.
- **Agents** narrow *who does what* and *when to hand off*; they point to skills and numbered rules.
- **Skills** encode *how* to name files, fill templates, validate, or commit—without replacing agent ownership.

## Collaboration model

- **Humans** own the contributor folder (e.g. `LTI-ICS/`) and PRs.
- **Product-oriented** edits → **`/product-manager`** (or its skills: `generate-prd`, plans/tasks for product phasing).
- **Technical design** → **`/architect`** + **`develop-architect`** (diagrams, typed ERD, ADRs).
- **Review before submit** → **`/documentation-auditor`** + **`validate-artifacts`** skill (structured report).
- **Never** use an agent to silently override another role’s ownership—use **handoffs** (see agent files).

## Rule precedence

Rules are ordered **`10-`** (foundation) through **`60-`** (validation governance). See **`10-project-overview.mdc`** for the stack table.

- **Narrower scope wins** for its topic (e.g. `20-deliverable-markdown.mdc` on `LTI-*/*.md` for deliverable sections).
- On conflict: **follow the rule**, not ad-hoc agent habits.
- **`alwaysApply: true`:** `10-`, `30-`, `40-`, `60-`. **`alwaysApply: false` (glob-scoped):** `20-` (`**/LTI-*/*.md`), `50-` (`LTI-*` + `ai-specs/**/*.md`).

---

## Agents

Invoke via Cursor’s agent picker (e.g. **`/architect`**, **`/product-manager`**, **`/documentation-auditor`**—exact UX depends on Cursor version).

### `architect`

| | |
|--|--|
| **Mission** | Turn agreed goals into coherent **technical** design: C4-aligned Mermaid, typed data models, NFRs, ADRs. |
| **When to use** | HLD, containers, deep C4 on one component, `erDiagram`, ADR updates, technical plans/tasks. |
| **When not to use** | Replacing product strategy, MVP calls, or PRD intent without PM alignment. |
| **Owns** | Technical structure, diagrams (with `50-diagram-standards.mdc`), `LTI-<slug>/ARD.md` when logging decisions. |
| **Does not own** | Lean Canvas, positioning, final prioritization. |
| **Handoffs** | To **`/product-manager`** for ambiguous requirements or prioritization; expects PRD/deliverable product sections for glossary alignment. |

### `product-manager`

| | |
|--|--|
| **Mission** | ATS-aware product narrative: pains, differentiation, PRD shape, use-case stories, MVP phasing themes. |
| **When to use** | PRD, goals, functions, Lean Canvas, use-case narratives, MoSCoW/themes. |
| **When not to use** | Final typed ERD, authoritative C4 depth, infrastructure truth—use **`/architect`**. |
| **Owns** | Product language, `generate-prd` output, leading product sections in `LTI-*.md`. |
| **Does not own** | ADRs, final architecture diagrams as engineering record. |
| **Handoffs** | To **`/architect`** for boundaries, typed models, sequence diagrams with stores/auth, deployment concerns. |

### `documentation-auditor`

| | |
|--|--|
| **Mission** | **Audit** docs: completeness, consistency, traceability, rule compliance—not ghostwriting. |
| **When to use** | Pre-submission review, after big merges, when artifacts may contradict each other. |
| **When not to use** | As substitute for PM or architect when the task is to **decide** product or architecture. |
| **Owns** | Findings reports, gap lists, compliance mapping to rules; default workflow uses **`validate-artifacts`** skill. |
| **Does not own** | Product strategy, final architecture, inventing requirements. |
| **Handoffs** | To **`/product-manager`** (ambiguous value/priorities); to **`/architect`** (technical inconsistency, missing ADRs). |

---

## Skills inventory

| Skill | Folder | Purpose | Primary agents | Create / update / validate |
|-------|--------|---------|----------------|----------------------------|
| **develop-architect** | [`skills/develop-architect/`](skills/develop-architect/) | Architecture drivers, C4 Mermaid, clean-architecture framing, ADR append rules | **`/architect`** | **Create/update** design text & diagrams |
| **generate-prd** | [`skills/generate-prd/`](skills/generate-prd/) | PRD template → `ai-specs/prd/<NNN>-prd.md` | **`/product-manager`** | **Create/update** PRD files |
| **plan-story** | [`skills/plan-story/`](skills/plan-story/) | Phased delivery plan → `ai-specs/plan/<NNN>-plan.md` | PM or architect (sequencing) | **Create** new plan file; **update** same `NNN` in place |
| **improve-story** | [`skills/improve-story/`](skills/improve-story/) | Task spec + AC → `ai-specs/tasks/<NNN>-task.md` | PM or architect | **Create** new task file; **update** same `NNN` in place |
| **validate-artifacts** | [`skills/validate-artifacts/`](skills/validate-artifacts/) | Cross-doc validation report; optional `ai-specs/review/<NNN>-review.md` | **`/documentation-auditor`** (default), anyone | **Validation-oriented** (read-only on sources unless user asks to apply fixes) |
| **commit** | [`skills/commit/`](skills/commit/) | Conventional commit messages | Any agent after doc changes | **Git snapshot** (not doc authoring) |

**When not to use:** Each skill’s `SKILL.md` has **When Not to Use**—e.g. `validate-artifacts` is not legal/compliance review; `commit` is not for fixing content without user intent.

---

## Rules overview (precedence order)

| File | Purpose | Scope / enforcement |
|------|---------|---------------------|
| **`10-project-overview.mdc`** | Repo purpose, LTI context, `LTI-*` layout, collaboration | Global + course layout; foundation |
| **`20-deliverable-markdown.mdc`** | Required sections in main deliverable + `prompts.md` quality | Glob: `**/LTI-*/*.md` |
| **`30-prompt-tracking.mdc`** | Mandatory append-only `prompts.md` log, format, failure behavior | Typically always-on; path per contributor slug |
| **`40-naming-and-paths.mdc`** | `ai-specs/.../<NNN>-*.md`, `LTI-<slug>/` basename match, forbid bare `-prd.md` stems | Global naming |
| **`50-diagram-standards.mdc`** | Mermaid + C4 semantic/visual consistency, grounding in requirements | `LTI-*` + `ai-specs` markdown with diagrams |
| **`60-review-and-validation.mdc`** | Validation before “complete”; alignment across artifacts | Governance to run validation passes |

---

## Recommended workflow (day-to-day)

1. **Read context:** root [`README.md`](../README.md), **`10-project-overview.mdc`**, your contributor folder convention (`LTI-<CONTRIBUTOR-SLUG>/`).
2. **Pick an agent** matching the task (product vs architecture vs audit)—see [Agents](#agents).
3. **Open the right skill(s)** from the agent definition or this guide; follow **Create vs Update** in each `SKILL.md` so you do not duplicate `NNN` files incorrectly.
4. **Produce or edit artifacts** in the approved paths (`40-naming-and-paths.mdc`).
5. **Validate:** use **`/documentation-auditor`** or apply **`validate-artifacts`** before claiming submission-ready (`60-review-and-validation.mdc`).
6. **Prompts:** every answered user message in Cursor workspaces using this rule set should append to **`LTI-<CONTRIBUTOR-SLUG>/prompts.md`** per **`30-prompt-tracking.mdc`** (assistant obligation).
7. **Commit** via **`commit`** skill when persisting to git; separate logical changes.
8. **Hand off** if you hit PM- or architect-owned decisions.

---

## Quick start (new contributor)

1. **Start here:** this document → skim [Agents](#agents), [Rules overview](#rules-overview-precedence-order), [Recommended workflow](#recommended-workflow-day-to-day).
2. **Course deliverable:** read **`20-deliverable-markdown.mdc`** and create **`LTI-<CONTRIBUTOR-SLUG>/LTI-<CONTRIBUTOR-SLUG>.md`** + **`prompts.md`** per **`10-project-overview.mdc`**.
3. **Choose an agent:** product writing → **`/product-manager`**; diagrams/ERD/C4/ADR → **`/architect`**; pre-submit check → **`/documentation-auditor`**.
4. **Avoid breaking conventions:** never use repository-root `prompts.md` for course prompts; use **`ai-specs/prd/<NNN>-prd.md`** not bare `-prd.md`.
5. **Before editing:** open the target **`SKILL.md`** for numbering rules; open **`40-naming-and-paths.mdc`** if unsure where a file belongs.

---

## Troubleshooting / common mistakes

| Mistake | Why it hurts | Fix |
|---------|----------------|-----|
| Wrong agent for the job | Scope creep, contradictions | Switch agent; use handoffs |
| Skipping validation | “Looks done” but inconsistent docs | Run **`validate-artifacts`** / **`/documentation-auditor`** |
| Ignoring rule precedence | Silent conflict with course requirements | Cite numbered rule; follow it |
| Wrong paths | Broken links, grader confusion | Use `40-naming-and-paths.mdc` patterns |
| New `NNN` on **edit** | Duplicate plans/tasks | **Update in place** per plan-story / improve-story |
| Forgetting prompt log | Fails course / audit trail | **`30-prompt-tracking.mdc`** |
| Inconsistent diagram names | Traceability breaks | **`50-diagram-standards.mdc`** + one glossary |
| Architect rewrites PRD intent | PM ownership violated | Hand off to **`/product-manager`** |

---

## Operability & maintenance checklist

Use when reviewing a PR or periodically auditing the repo tooling.

- [ ] All **`.cursor/rules/`** references in **`.cursor/agents/*.md`** use **numbered** filenames (`10-`, `20-`, …)—no stale `project-overview.mdc`-style paths.
- [ ] Each **agent** points to **real** skill paths under **`.cursor/skills/`**.
- [ ] **Path conventions** in rules, skills, and docs agree (`<NNN>` three-digit, `LTI-<CONTRIBUTOR-SLUG>/`).
- [ ] **`documentation-auditor`** still defaults to **`validate-artifacts`** for full audits (see agent file).
- [ ] **`.cursor/README.md`** still lists every agent and every skill folder present on disk.
- [ ] Root [`README.md`](../README.md) still links to this guide (for Cursor users).
- [ ] After adding a rule: assign a **new number** in sequence, update this README’s rules table and `10-project-overview.mdc` stack if needed.
- [ ] After adding an agent: document it here under [Agents](#agents).

---

## Examples (short)

**Create a PRD**  
→ Agent: **`/product-manager`**. Skill: **`generate-prd`**. Output: `ai-specs/prd/<NNN>-prd.md`. Then lift sections into `LTI-<slug>/LTI-<slug>.md` if that’s your single deliverable.

**Refine a story into a task**  
→ Skill: **`improve-story`**. Output: `ai-specs/tasks/<NNN>-task.md`. Agent: PM or architect depending on whether AC is product- or tech-led.

**Develop architecture (HLD, ERD, C4, ADRs)**  
→ Agent: **`/architect`**. Skill: **`develop-architect`**. Rules: **`50-diagram-standards.mdc`**, **`20-deliverable-markdown.mdc`** for course sections. ADRs: `LTI-<slug>/ARD.md`.

**Audit before submission**  
→ Agent: **`/documentation-auditor`**. Skill: **`validate-artifacts`** (read first; emit full **Validation report**). Optional save: `ai-specs/review/<NNN>-review.md`.

---

## Extending this setup safely

1. **Rules first** if behavior must be **mandatory** for all assistants in scope.
2. **Skills** for repeatable **file/process** patterns (templates, numbering, validation steps).
3. **Agents** for **role boundaries** and handoffs—keep them thin; link to skills and numbered rules.
4. Update **this README** and **`10-project-overview.mdc`** when the stack changes.
5. Run the [Operability checklist](#operability--maintenance-checklist) after changes.

---

## Related documentation

- Course brief: repository root [`README.md`](../README.md)
- Contributor prompt log: `LTI-<CONTRIBUTOR-SLUG>/prompts.md` (per **`30-prompt-tracking.mdc`**)
