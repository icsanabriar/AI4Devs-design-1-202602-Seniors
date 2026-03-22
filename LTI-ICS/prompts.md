# Prompts log

# Prompt - 2026-03-22T00:00:37Z
## Agent: Composer
The main components or stages of an Applicant Tracking System (ATS) are:

1. Job creation: Create the job openings or positions to be filled.
2. Job posting: Publish job openings on job boards, company websites, social media, and other channels.
3. Application intake: Receive and collect candidate applications.
4. Application review: Screen and evaluate resumes or candidate profiles.
5. Online assessments: Conduct technical, psychometric, or knowledge-based tests.
6. Interview scheduling: Coordinate interview dates and times with candidates.
7. Hiring selected candidates: Choose the best candidates and complete the hiring process.

Based on the previous context,  @.cursor/agents/product-manager.md @.cursor/skills/generate-prd/SKILL.md

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
