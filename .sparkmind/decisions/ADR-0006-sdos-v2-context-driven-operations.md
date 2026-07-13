# ADR-0006: SDOS v2 — Context-Driven, Single-State Operations

> **Version**: 1.0 · **Status**: Accepted
> **Date**: 2026-07-13 · **Decision owner**: Founder/CTO

## Context

SDOS v1.1 preserved project knowledge but imposed excessive routine work. An engineer was instructed to load at least six context sources and, after ordinary sessions, potentially update state, current sprint, changelog, sprint detail, decision log, and an engineering report. Sprint 002 showed this duplicated state, consumed AI context/credits, and made session completion slower than necessary.

ADR-0002 remains valid: durable knowledge belongs in the repository, not a long system prompt. Its original folder structure and mandatory-update consequences require refinement.

## Decision

Adopt SDOS v2 with these rules:

1. `CURRENT_STATE.md` owns active sprint, current task, progress, blockers, and next action.
2. Remove `CURRENT_SPRINT.md`; sprint details remain in the linked sprint file.
3. Use lazy task-based context routing from `.sparkmind/README.md`; only `CURRENT_STATE.md` is universal startup context.
4. Merge session and Git lifecycle into `WORKFLOW.md`.
5. Merge engineering, repository, source-code, and environment standards into `standards/engineering.md`.
6. Use one temporary `SESSION_HANDOFF.md` only for interrupted work.
7. Update `CHANGELOG.md` and create Engineering Reports only at milestone/sprint closure.
8. Create documentation progressively; do not maintain empty proposal structures.
9. Every active context has a named canonical owner and update trigger.

## Consequences

### Positive

- One routine state update instead of several synchronized status files.
- Two-document default startup path (`CURRENT_STATE.md` + task-relevant workflow/context).
- Faster AI onboarding and recovery with less context loading.
- Fewer broken-reference and stale-status risks.
- Historical ADRs, reports, and sprints remain preserved.

### Trade-offs

- Readers must follow links for detail rather than receiving a duplicated summary everywhere.
- `CURRENT_STATE.md` must remain concise and truthful.
- Lazy loading requires engineers to classify their task before opening context.

## Supersedes

This ADR partially supersedes ADR-0002 only for the SDOS folder layout, mandatory full-context startup, and per-session reporting/update burden. ADR-0002's repository-as-source-of-truth decision remains accepted.

## Validation

Review after two product sprints using:

- number of routinely touched governance files per session (target: 1),
- default startup documents (target: 1–2 plus task-specific context),
- broken local documentation links (target: 0),
- handoff recovery without chat history (target: successful).
