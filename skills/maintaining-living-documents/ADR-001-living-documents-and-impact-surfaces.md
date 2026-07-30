# ADR-001 — Use Living Documents and Impact Surfaces for Agent Planning Artifacts

Status: accepted
Decided: 2026-07-28
Scope: Superpowers skills that create, execute, or modify durable documents, records, or agent-facing guidance.

## Context

A human partner reported that Superpowers-generated specs, implementation plans, and ADR-like documents branch into multiple dated versions. Once branching happens, later agents may not use prior documents well, the user must decide which document to point agents at, and reading many documents increases token cost.

The baseline skill review confirmed the behavior is encoded in the current contracts:

- `brainstorming` writes `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`.
- `writing-plans` writes `docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md`.
- `executing-plans` and `subagent-driven-development` execute the active plan and record execution trace, but do not require canonical knowledge updates.
- `writing-skills` requires RED-GREEN-REFACTOR for skill edits, but does not require decision records, inline decision comments, or impact-surface identification.

## Decision

Superpowers will treat durable planning and guidance artifacts as living documents by default, not as a growing set of competing dated branches. `maintaining-living-documents` means keeping the authoritative document current, recording why it changed, and demoting stale material to archived records only when retention is needed.

This is plain content governance/content lifecycle practice applied to agent work. It overlaps with records management only when a historical state must be preserved as evidence or release-specific reference.

1. Durable guidance is organized by feature or domain and abstraction level when a project defines that layout. If no layout is defined, agents discover the authoritative source from README files, AGENTS/instruction files, docs indexes, nearby ADRs/decision records, and linked project documents before creating any default structure.
2. Living documents are updated in place and carry a bounded change log or nearby decision comment.
3. Dated specs and plans are execution snapshots, not the default durable source of truth.
4. Versioned copies are created only for concrete archival need: release-specific behavior, legal/audit retention, historical comparison, rollback, or explicit user request.
5. The first archived version in a repository requires choosing one convention: semantic, datetime, or incremental. Existing conventions continue unchanged.
6. Archive filenames place the version between basename and extension, using a sortable segment such as `name.v001.002.003.md`, `name.2026-07-29T153000Z.md`, or `name.r0001.md`.
7. Repeated or blocking conflicts trigger a decision session: conflict statement, alternatives, tradeoffs, decision, and document update.
8. Each document-affecting task records an impact surface covering code, skills, docs, decisions, archive/versioning, verification, and no-update rationale.
9. Process-changing skill edits add short inline comments that name this ADR or a later governing ADR.

## Consequences

Future agents should read the project instructions, relevant current document, and directly referenced decisions instead of scanning many dated artifacts. The living document carries the operational truth; archived records preserve why and when the truth changed.

This reduces token use and user routing burden, but it requires disciplined change-log entries, impact-surface updates, and clear archive labels. If those are skipped, stale records can masquerade as current guidance.

## Affected Skills

- `maintaining-living-documents`: governing workflow.
- `using-superpowers`: adds a short routing gate.
- `brainstorming`: replaces default dated design-spec output with living-document update.
- `writing-plans`: treats persistent plans as snapshots, not default canonical docs.
- `executing-plans`: checks impact surface before closing execution.
- `subagent-driven-development`: carries impact-surface and decision references through briefs, ledgers, and reviews.
- `writing-skills`: requires decision records and inline comments for process-changing skill edits.
- `requesting-code-review`: examples reference the scratch execution snapshot and governing living documents instead of a permanent dated plan.

## Verification Scenarios

The original pressure checks covered three failure modes: design work defaulting to permanent dated specs, execution work closing without document impact updates, and skill edits lacking decision trace. The current policy adds archive/version convention selection and filename ordering checks.
