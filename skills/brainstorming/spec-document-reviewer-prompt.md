# Design Document Reviewer Prompt Template

Use this template when dispatching a living design document reviewer subagent.

<!-- ADR-001: reviewer now checks canonical living documents instead of dated specs. -->
**Purpose:** Verify the updated living document is complete, consistent, and ready for implementation planning.

**Dispatch after:** Canonical living document is updated.

```
Subagent (general-purpose):
  description: "Review living design document"
  prompt: |
    You are a living design document reviewer. Verify this document is complete and ready for planning.

    **Document to review:** [DOCUMENT_FILE_PATH]

    ## What to Check

    | Category | What to Look For |
    |----------|------------------|
    | Completeness | TODOs, placeholders, "TBD", incomplete sections |
    | Consistency | Internal contradictions, conflicting requirements |
    | Clarity | Requirements ambiguous enough to cause someone to build the wrong thing |
    | Scope | Focused enough for a single execution contract — not covering multiple independent subsystems |
    | Impact Surface | Affected code, skills, docs, decisions, verification, and no-update rationale are named |

    ## Calibration

    **Only flag issues that would cause real problems during implementation planning.**
    A missing section, a contradiction, or a requirement so ambiguous it could be
    interpreted two different ways — those are issues. Minor wording improvements,
    stylistic preferences, and "sections less detailed than others" are not.

    Approve unless there are serious gaps that would lead to a flawed plan.

    ## Output Format

    ## Document Review

    **Status:** Approved | Issues Found

    **Issues (if any):**
    - [Section X]: [specific issue] - [why it matters for planning]

    **Recommendations (advisory, do not block approval):**
    - [suggestions for improvement]
```

**Reviewer returns:** Status, Issues (if any), Recommendations
