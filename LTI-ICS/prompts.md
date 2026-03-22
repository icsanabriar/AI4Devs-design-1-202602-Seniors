# Prompts log

# Prompt - 2026-03-22T00:00:37Z
## Agent: Composer
Frame the PRD around the seven ATS lifecycle stages (see `ATS-Lifecycle.md` in this folder for the numbered list).

Based on the previous context, @.cursor/agents/product-manager.md @.cursor/skills/generate-prd/SKILL.md

---
# Prompt - 2026-03-22T00:04:13Z
## Agent: Composer
Based on @LTI-ICS/001-prd.md @.cursor/agents/architect.md @.cursor/skills/develop-architect/SKILL.md

---
# Prompt - 2026-03-22T00:09:54Z
## Agent: Composer
Based on the @LTI-ICS/001-prd.md @LTI-ICS/ARD.md and @LTI-ICS/LTI-ICS.md @.cursor/agents/documentation-auditor.md @.cursor/skills/validate-artifacts/SKILL.md

---
# Prompt - 2026-03-22T00:13:16Z
## Agent: Composer
@.cursor/agents/architect.md there are some inconsistencies that needs to be fixed:
FR-026 (automation audit log: rule id, actor/system, timestamp) — LTI-ICS.md C4 component text references automation_run logging, but erDiagram has no AUTOMATION_RUN / AUTOMATION_AUDIT (or equivalent) entity — FAIL for full FR ↔ data-model traceability (severity: major for audit story completeness).
FR-020 (start date, requisition fill) — APPLICATION has outcome_code but no explicit start_date / hired_at (or similar); JOB_REQUISITION has no explicit filled_count / filled_at — FAIL partial (severity: major until fields or JSON payload convention is documented).
FR-001 (hiring team) — No requisition–user membership (e.g. hiring team / role on req) in ER — FAIL partial (severity: major unless intentionally deferred with explicit "Open question" in architecture doc).

---
# Prompt - 2026-03-22T00:15:56Z
## Agent: Composer
Based on the @LTI-ICS/001-prd.md @LTI-ICS/ARD.md and @LTI-ICS/LTI-ICS.md @.cursor/agents/documentation-auditor.md @.cursor/skills/validate-artifacts/SKILL.md

---
# Prompt - 2026-03-22T00:18:38Z
## Agent: Composer
@.cursor/agents/product-manager.md In 001-prd.md, under Risks, assumptions, dependencies, add that multi-tenant row-level organization_id is the chosen MVP posture (ADR-002) so PRD and ADR do not read as "still undecided."

---
# Prompt - 2026-03-22T00:20:46Z
## Agent: Composer
@.cursor/agents/architect.md In LTI-ICS.md → Data model → Notes, one sentence on FR-001 non-team fields (department, location, employment type) living in description_json or a follow-up normalization—closes the minor PRD ↔ ER gap.

---
# Prompt - 2026-03-22T00:21:33Z
## Agent: Composer
@.cursor/agents/architect.md If FR-010 “owner” is literal product language, either add owner_user_id (nullable) on APPLICATION or state that owner is derived (e.g. primary recruiter on job_requisition_member).

---
# Prompt - 2026-03-22T00:22:59Z
## Agent: Composer
Based on the @LTI-ICS/001-prd.md @LTI-ICS/ARD.md and @LTI-ICS/LTI-ICS.md @.cursor/agents/documentation-auditor.md @.cursor/skills/validate-artifacts/SKILL.md

---
# Prompt - 2026-03-22T00:24:15Z
## Agent: Composer
@.cursor/skills/commit/SKILL.md

---
# Prompt - 2026-03-22T02:04:18Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/agents/documentation-auditor.md around lines 122 - 123, The current
phrase "**Conflicting instructions** from user vs rules—state the conflict and
**default to rules** unless user explicitly overrides for the session." weakens
governance by permitting overrides; update the wording so it disallows bypassing
always-apply constraints: replace that sentence with language that clarifies the
agent must state the conflict and default to rules, allows the user only to
narrow the scope of non-always-apply instructions, and explicitly prohibits any
user override that would negate or bypass always-apply rules (reference the
phrase "**Conflicting instructions**" and the "default to rules" logic to locate
and update the sentence).

---
# Prompt - 2026-03-22T02:11:13Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/README.md at line 7, The heading "Path patterns: what is real vs
example" is using an H3 (###) directly after the H1, breaking the markdown
hierarchy; change that heading to H2 (replace `### Path patterns: what is real
vs example` with `## Path patterns: what is real vs example`) so the document
follows proper heading levels and passes markdown linting.

---
# Prompt - 2026-03-22T02:16:38Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/README.md around lines 173 - 191, The table rows in
.cursor/README.md (the setup-check and Rules overview) are malformed because
unescaped pipes and improperly closed code spans break Markdown rendering; fix
by ensuring every filename and pattern (e.g.
.cursor/rules/10-project-overview.mdc, .cursor/agents/architect.md,
.cursor/skills/commit/SKILL.md, <CONTRIBUTOR-SLUG>, NNN, -prd.md) is either
wrapped in a proper code span or has internal pipes escaped (use `\|`), and make
sure backticks are balanced for cells like `.cursor/rules/10-` … `60-`.mdc` and
the table header rows so each cell is valid Markdown and the columns align
correctly.

---
# Prompt - 2026-03-22T02:17:32Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/rules/20-deliverable-markdown.mdc around lines 3 - 30, The rule
currently applies to any markdown under LTI-*/ which causes false failures for
prompts.md, PRDs, ADRs; update the globs and rule scoping so the main-document
requirements only run against the main deliverable filename (change "globs:
\"**/LTI-*/*.md\"" to a more specific pattern such as "globs:
\"**/LTI-*/LTI-*.md\"" or add an include for "LTI-<CONTRIBUTOR-SLUG>.md" and add
a separate rule or exclude pattern for "prompts.md" (and other non-deliverable
docs) so the section that mandates items 1–7 only validates files matching
LTI-<CONTRIBUTOR-SLUG>.md; ensure prompts.md continues to be matched by its own
rule (or excluded) to avoid the main-document checks running against it.

---
# Prompt - 2026-03-22T02:20:27Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/rules/40-naming-and-paths.mdc at line 43, Line currently points ADR
append-only rules at 50-diagram-standards.mdc which is about diagrams; update
the cross-reference so the ADR append-only guidance points to the correct ADR
lifecycle doc instead of 50-diagram-standards.mdc. Replace the reference in the
sentence containing "LTI-<CONTRIBUTOR-SLUG>/ARD.md" so it cites the canonical
ADR lifecycle file (the document that defines ADR append-only rules — e.g., the
ADR lifecycle or architecture decision records guideline) and ensure the wording
still enforces "append-only ADRs" for LTI-<CONTRIBUTOR-SLUG>/ARD.md.

---
# Prompt - 2026-03-22T02:22:09Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/rules/60-review-and-validation.mdc around lines 24 - 31, Update the
validation checklist in .cursor/rules/60-review-and-validation.mdc to explicitly
enforce prompt-tracking compliance by adding a rule that, when a submission is
in scope, verifies the existence and correct format of
.cursor/rules/30-prompt-tracking.mdc artifacts and contributor prompt files
(LTI-<CONTRIBUTOR-SLUG>/prompts.md); modify the checklist (e.g., add a new
bullet after "Path compliance" or augment item 1) to require presence/format
checks and fail the audit if the prompt-tracking file or properly named
LTI-.../prompts.md is missing or malformed, and reference the exact filenames
(.cursor/rules/30-prompt-tracking.mdc and LTI-<CONTRIBUTOR-SLUG>/prompts.md) so
reviewers and automated validators can locate and validate them.

---
# Prompt - 2026-03-22T02:26:03Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/skills/commit/SKILL.md around lines 49 - 60, The commit message
template in the SKILL.md snippet is inconsistent: the template line "(<scope>):
<Imperative description with lowercase after the colon>" conflicts with the
example "feat(dn): Add new diagram for candidates component" and the note saying
the first word after ':' must be capitalized. Pick one convention and make the
text consistent: either change the template to require a capitalized first word
(e.g., "(<scope>): <Imperative description with Capitalized first word>") or
change the example and explanatory note to require lowercase; update the
template line, the example string "feat(dn): Add new diagram for candidates
component", and the descriptive bullet that mentions "first word after `:` is
capitalized" so all three use the same rule.

---
# Prompt - 2026-03-22T02:27:46Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/skills/generate-prd/SKILL.md around lines 55 - 103, The PRD template
under "PRD template (required sections)" is missing the mandatory Lean Canvas
and exactly three use-case entries (with diagrams) that are required elsewhere;
update the template to include a "Lean Canvas" subsection and a "Use cases"
subsection that explicitly requires exactly three primary use cases (each with a
short description and a placeholder for an accompanying diagram), and clarify
these as required for course-aligned PRDs so generated documents cannot pass
validation without them.

---
# Prompt - 2026-03-22T02:29:14Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In `@LTI-ICS/001-prd.md` around lines 124 - 145, Add a new NFR section for
candidate PII privacy lifecycle to cover retention and deletion: create explicit
requirements (e.g., NFR-008) that specify retention windows for applicant data,
automated and manual deletion/erasure flows, handling of consent withdrawal,
data minimization, export/portability, and secure purge procedures, and link
these to existing controls (reference NFR-001 RBAC and NFR-002 audit trails) so
that deletion actions are auditable and retention rules are enforced by the
system.

---
# Prompt - 2026-03-22T02:31:28Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In `@LTI-ICS/001-prd.md` around lines 289 - 299, Update the conceptual model to
consistently reflect tenant scoping by marking tenant-owned entities as
organization-scoped and adding organization_id where missing: add
organization_id (or indicate "belongs to Organization") to JobRequisition,
JobPosting, Application, Interview, Feedback, and AuditEvent in the
table/diagram (also verify Candidate if it can be organization-scoped in your
domain), and ensure AutomationRule and User remain explicitly scoped; keep the
naming consistent with the stated organization_id strategy so all tenant-owned
records are clearly tied to Organization.

---
# Prompt - 2026-03-22T02:32:20Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In `@LTI-ICS/prompts.md` around lines 5 - 15, The prompt file contains
assistant-like generated answer text in the block starting with "The main
components or stages of an Applicant Tracking System (ATS) are:" (lines 5–14);
remove that assistant-style content so the prompt log contains only the original
user prompt text, and if you need to preserve the ATS list for context move it
into a separate assistant/response artifact rather than the prompt body. Ensure
the block is replaced with a clean user-only prompt placeholder or instruction,
and verify no other generated-answer phrasing remains in the prompt content.

---
# Prompt - 2026-03-22T02:44:41Z
## Agent: Composer
@.cursor/agents/documentation-auditor.md @.cursor/skills/validate-artifacts/SKILL.md

---
# Prompt - 2026-03-22T02:47:52Z
## Agent: Composer
@.cursor/skills/commit/SKILL.md

---
# Prompt - 2026-03-22T02:57:35Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/skills/commit/SKILL.md around lines 49 - 60, The commit message
template in the SKILL.md snippet is inconsistent: the template line "(<scope>):
<Imperative description with lowercase after the colon>" conflicts with the
example "feat(dn): Add new diagram for candidates component" and the note saying
the first word after ':' must be capitalized. Pick one convention and make the
text consistent: either change the template to require a capitalized first word
(e.g., "(<scope>): <Imperative description with Capitalized first word>") or
change the example and explanatory note to require lowercase; update the
template line, the example string "feat(dn): Add new diagram for candidates
component", and the descriptive bullet that mentions "first word after `:` is
capitalized" so all three use the same rule.

---
# Prompt - 2026-03-22T02:59:59Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/agents/documentation-auditor.md at line 90, The Markdown table row
contains an unescaped pipe in the code span
"ai-specs/plan|tasks|review/<NNN>-*.md" which breaks the table; update the table
row in .cursor/agents/documentation-auditor.md to either escape the pipes (e.g.,
replace | with \| inside the code span) or split into multiple inline code spans
like `ai-specs/plan` / `tasks` / `review/<NNN>-*.md`, making sure the row still
references the LTI directory rule in .cursor/rules/40-naming-and-paths.mdc and
keeps the basename match note intact.

---
# Prompt - 2026-03-22T03:00:59Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/skills/generate-prd/SKILL.md at line 59, The wording in SKILL.md
overstates what validate-artifacts enforces: update the "Course-aligned PRDs"
sentence so it no longer claims that missing/placeholder Mermaid diagrams or
skimpy third use cases "do not satisfy .cursor/rules/20-deliverable-markdown.mdc
/ validate-artifacts expectations"; instead, make the statement accurate by
specifying that the validator currently checks for section presence (e.g., "##
Lean Canvas" and "## Use cases") and that completeness/diagram quality may be
reviewed by downstream processes or manual audit; reference the same header text
"Course-aligned PRDs" and the validator name validate-artifacts in the revision
to keep context.

---
# Prompt - 2026-03-22T03:03:15Z
## Agent: Composer
@Commit all

---
# Prompt - 2026-03-22T03:09:38Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/skills/commit/SKILL.md around lines 49 - 60, The commit message
template in the SKILL.md snippet is inconsistent: the template line "(<scope>):
<Imperative description with lowercase after the colon>" conflicts with the
example "feat(dn): Add new diagram for candidates component" and the note saying
the first word after ':' must be capitalized. Pick one convention and make the
text consistent: either change the template to require a capitalized first word
(e.g., "(<scope>): <Imperative description with Capitalized first word>") or
change the example and explanatory note to require lowercase; update the
template line, the example string "feat(dn): Add new diagram for candidates
component", and the descriptive bullet that mentions "first word after `:` is
capitalized" so all three use the same rule.

---
# Prompt - 2026-03-22T03:10:44Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/agents/documentation-auditor.md around lines 43 - 44, The
documentation-auditor spec uses two different verdict vocabularies; standardize
them to a single set (preferably the one defined for validate-artifacts).
Replace the later occurrences that read "Not ready / Ready with findings /
Blocked" with "Pass / Pass with findings / Blocked" so the validate-artifacts
procedure, verdicts, and any references to ai-specs/review/<NNN>-review.md all
use the same vocabulary (search for "validate-artifacts" and the alternate
wording to locate the mismatches and update them).

---
# Prompt - 2026-03-22T03:11:49Z
## Agent: Composer
@.cursor/skills/commit/SKILL.md all

---
# Prompt - 2026-03-22T03:34:04Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/skills/commit/SKILL.md around lines 49 - 60, The commit message
template in the SKILL.md snippet is inconsistent: the template line "(<scope>):
<Imperative description with lowercase after the colon>" conflicts with the
example "feat(dn): Add new diagram for candidates component" and the note saying
the first word after ':' must be capitalized. Pick one convention and make the
text consistent: either change the template to require a capitalized first word
(e.g., "(<scope>): <Imperative description with Capitalized first word>") or
change the example and explanatory note to require lowercase; update the
template line, the example string "feat(dn): Add new diagram for candidates
component", and the descriptive bullet that mentions "first word after `:` is
capitalized" so all three use the same rule.

---
# Prompt - 2026-03-22T04:00:00Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In @.cursor/agents/documentation-auditor.md at line 66, Update the ADR filename
referenced in the auditors table: replace the typo
"LTI-<CONTRIBUTOR-SLUG>/ARD.md" with the correct "LTI-<CONTRIBUTOR-SLUG>/ADR.md"
wherever it appears (the table entry under "ADRs" currently uses ARD.md). Ensure
all occurrences in this document that reference ARD.md are corrected so ADR
checks won't break.

---
# Prompt - 2026-03-22T03:43:28Z
## Agent: Composer
Review all references to @LTI-ICS/ARD.md The filename is wrong, it should be ADR.md. Rename the file and update all the references in all required files.

---
# Prompt - 2026-03-22T03:45:44Z
## Agent: Composer
Rename the file @LTI-ICS/reference-ats-lifecycle-stages.md to ATS-Lifecycle.md and update all the references in all required files.

---
# Prompt - 2026-03-22T03:47:32Z
## Agent: Composer
@.cursor/skills/commit/SKILL.md all

---
# Prompt - 2026-03-22T03:48:39Z
## Agent: Composer
@.cursor/agents/documentation-auditor.md @.cursor/skills/validate-artifacts/SKILL.md 

---
# Prompt - 2026-03-22T03:50:50Z
## Agent: Composer
@.cursor/agents/product-manager.md Renumber or reorder NFR-* so IDs increase monotonically (or add a one-line note that numbering follows subsection insert order)

---
# Prompt - 2026-03-22T03:51:44Z
## Agent: Composer
at @LTI-ICS/prompts.md update the reference from eference-ats-lifecycle-stages.md to ATS-Lifecycle.md

---
# Prompt - 2026-03-22T03:52:24Z
## Agent: Composer
@.cursor/agents/documentation-auditor.md @.cursor/skills/validate-artifacts/SKILL.md 

---
# Prompt - 2026-03-22T03:53:55Z
## Agent: Composer
Same for NFR-008 vs retention in an old prompt: leave as archive or append a one-line clarification that NFR IDs were renumbered in PRD v0.5.

**Reviewer note (PRD v0.5):** **001-prd.md** v0.5 (2026-03-22) defines **NFR-001–NFR-011** in section order; older prompts that cite **NFR-008** for **retention** refer to the requirement now **NFR-003**; **NFR-008** is **RTO/RPO**.

---
# Prompt - 2026-03-22T03:54:32Z
## Agent: Composer
@.cursor/skills/commit/SKILL.md 

---
# Prompt - 2026-03-22T04:06:10Z
## Agent: Composer
Verify each finding against the current code and only fix it if needed.

In `@LTI-ICS/ADR.md` around lines 64 - 77, ADR-004 is marked "Proposed" but the
repository's architecture narrative already assumes Redis pub/sub is adopted;
update ADR-004 by changing its Status from "Proposed" to "Accepted" and add a
short note in the ADR Decision/Consequences sections reflecting the current
implemented behavior (Redis pub/sub fan-out and WebSocket termination), or
alternatively insert a clear conditional statement into the LTI-ICS architecture
narrative that indicates Redis pub/sub is assumed only if ADR-004 is accepted;
reference ADR-004, the "Decision" and "Consequences" paragraphs in ADR.md and
the LTI-ICS architecture section that mentions Redis pub/sub to keep the
documents consistent.

---
# Prompt - 2026-03-22T04:07:55Z
## Agent: Composer
@.cursor/agents/documentation-auditor.md @.cursor/skills/validate-artifacts/SKILL.md 

---
# Prompt - 2026-03-22T04:09:12Z
## Agent: Composer
@.cursor/skills/commit/SKILL.md 
