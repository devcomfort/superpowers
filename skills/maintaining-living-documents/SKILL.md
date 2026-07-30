---
name: maintaining-living-documents
description: Use when creating or changing documentation, docs, durable documents, records, specs, plans, ADRs, README, runbooks, prompts, skills, diagrams, agent-facing guidance, or when editing, updating, renaming, archiving, versioning, reconciling, reviewing, or relying on them
---

# Maintaining Living Documents

<!-- ADR-001: establishes canonical living documents, decision sessions, impact surfaces, and controlled archive/version handling for Superpowers planning artifacts. -->

## Purpose

Maintaining living documents means keeping one current, authoritative document for each durable guidance surface, recording why it changed, and demoting stale material to archived records only when retention is needed. It is not a new framework: it applies content governance and content lifecycle practices to agent work, and uses records-management terms when a historical copy must be retained.

Use **living document** for current, actionable guidance. Use **record** or **archive** for preserved history that must not be mistaken for current guidance.

## When to run

Run this checklist for any task that creates, edits, updates, renames, reviews, reconciles, versions, archives, or relies on:

- specs, requirements, proposals, or product guidance;
- implementation plans, execution contracts, runbooks, or operational notes;
- ADRs, decision records, change logs, or audit/history records;
- README files, user docs, diagrams, prompts, skills, harness rules, or agent-facing instructions.

Do not run it for disposable command output or scratch notes unless they affect future decisions or guidance.

## Required steps

1. **Classify the artifact.** Decide whether it is current guidance, historical rationale, an execution snapshot, an archived record, or disposable output.
2. **Find the authoritative source.** Follow project instructions first. If no layout is defined, discover it from README files, AGENTS/instruction files, docs indexes, nearby ADRs/decision records, and linked project documents before creating any default structure.
3. **Read narrowly.** Read the index, target document, and directly referenced decisions. Expand only when the impact surface shows another artifact is affected.
4. **Keep the living document current.** Update the canonical document in place. Do not create a parallel version just because the current document is stale.
5. **Record intent.** Add a bounded change-log entry or nearby Markdown comment with date, summary, reason, and governing decision if any.
6. **Version only for archival need.** Create a versioned copy only when a previous state must remain usable for release-specific behavior, legal/audit retention, historical comparison, rollback, or an explicit user request.
7. **Choose the version convention.** If the repository already records a convention, follow it. If not, ask the user once before creating the first versioned archive: semantic, datetime, or incremental.
8. **Name archived versions for sorting.** Put the version between basename and extension: `name.<version>.ext`. Choose a representation that sorts oldest to newest in normal filename order.
9. **Close the impact surface.** Fill the template below before reporting completion.

## Version conventions

| Convention | Use when | Filename segment |
|---|---|---|
| Semantic | meaning changes by major/minor/patch level | `v1.2.3`; if lexical sort across multi-digit values matters, use a fixed-width archive segment like `v001.002.003` and record canonical SemVer `1.2.3` inside the file |
| Datetime | publication/effective time is the clearest identity | `2026-07-29T153000Z` |
| Incremental | simple ordered archives are enough | `r0001`, `r0002`, `r0003` |

Examples: `routing.v001.002.003.md`, `routing.2026-07-29T153000Z.md`, `routing.r0003.md`.

## Impact Surface template

```markdown
## Impact Surface
- Code:
- Skills:
- Docs:
- Decisions:
- Archive/versioning:
- Verification:
- No-update rationale:
```

Use deterministic checks first: referenced paths exist, skill names resolve, ADR IDs exist, archived records are not linked as current guidance, and status values are consistent. Then use judgment for stale requirements, superseded assumptions, incompatible instructions, or missing downstream docs.

## Decision Session trigger

Start a decision session when any of these block progress:

- two current sources disagree;
- a new request contradicts an accepted decision;
- the authoritative source cannot be chosen without design judgment;
- repeated archive/version requests suggest competing current truths;
- a plan/review conflict changes process behavior.

Decision session workflow: state the conflict, list options, compare tradeoffs, ask for or record the final decision, update current guidance, update or create the decision record, and add inline decision comments to modified skill docs.

## Process-changing skill edits

For process-changing skill edits, add a short Markdown comment near each changed section:

```markdown
<!-- ADR-001: replaced dated spec/plan artifact gate with living-document update gate. -->
```

Comments name the decision that caused the change; the prose still explains the behavior plainly.

## Close-out checks

- Living document guidance lives in one authoritative place.
- Stale material is labeled as an archived record or has been folded into current guidance.
- Versioned copies exist only for a concrete archival need and follow the chosen convention.
- Impact Surface is complete or has a concrete no-update rationale.
- Repeated conflicts triggered a decision session instead of another document branch.
