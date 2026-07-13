# Architecture Improvement Report: SDOS v2

> **Version**: 1.0 · **Status**: Final · **Date**: 2026-07-13
> **Owner**: Engineering

## Executive Summary

SDOS v1.1 successfully made the repository the source of truth, but its operational architecture was documentation-driven: six startup sources, overlapping state documents, multiple workflow/standard files, and broad per-session update requirements. SDOS v2 preserves all durable history and decisions while replacing the runtime layer with context-driven navigation, one operational state, one workflow, two standards, and one temporary handoff.

## Audit Baseline

At audit start, `.sparkmind/` plus `docs/` contained **36 Markdown files and 2,348 lines**.

| Finding | Evidence | Cost |
|---|---|---|
| Mandatory full-context loading | SDOS README required constitution, state, current sprint, decision log, all context, and session workflow | High token/time cost before small tasks |
| Split operational state | `STATE.md` repeated active sprint, blockers, backlog also present in `CURRENT_SPRINT.md` and sprint index | Stale and contradictory facts |
| Excessive update fan-out | Session workflow/Constitution expected state, sprint pointer, changelog, sprint file, report, and sometimes ADR updates | 20–30% administrative effort observed in Sprint 002 handoff context |
| Workflow fragmentation | Session lifecycle and Git workflow repeated review, commit, and cleanliness rules | Navigation and maintenance overhead |
| Standard fragmentation | Engineering, repository, source-code, and environment docs overlapped structure, secrets, dependencies, and checks | Four files needed for one code task |
| Premature structure | Empty proposals index/template and technical docs index existed without active content | More files without delivery value |
| Report churn | Report required per mission and later edit to insert commit hash | Extra commit and duplicated Git provenance |
| Stale references | Repository standard still described pre-Sprint-002 root; many links pointed to operational files slated for consolidation | Broken-reference risk |

## Target Architecture

```text
CURRENT_STATE (universal, current truth)
      │
      ├── WORKFLOW (execution contract)
      ├── task-specific standard/doc
      ├── relevant ADR only
      ├── active sprint details only
      └── SESSION_HANDOFF only when active
```

### Canonical Ownership

- Operational status: `CURRENT_STATE.md`.
- Workflow and Git: `WORKFLOW.md`.
- Code/repository/environment rules: `standards/engineering.md`.
- Documentation ownership/triggers: `standards/documentation.md`.
- Durable decisions: `DECISION_LOG.md` + ADRs.
- Milestones: root `CHANGELOG.md`.
- Evidence: sprint-level reports.

## Structural Changes

### Consolidated

- `STATE.md` + `CURRENT_SPRINT.md` → `CURRENT_STATE.md`.
- Two workflow files → `WORKFLOW.md`.
- Four engineering/repository/source/environment standards → `standards/engineering.md`.
- ADR folder rules → `DECISION_LOG.md`.

### Removed

- Redundant `docs/README.md` and `decisions/README.md` pointer files.
- Empty `proposals/` index and premature proposal template.
- Superseded split workflow and standard files.

### Added

- `SESSION_HANDOFF.md` as an empty-by-default recovery contract.
- Task-based context router and ownership map.
- ADR-0006 to preserve rationale and review metrics.

## Impact

Before adding this audit evidence, active restructuring reduced the measured surface to **30 files and 1,953 lines** (from 36/2,348), while preserving historical sprint/report/ADR archives. More importantly:

| Metric | v1.1 | v2 target |
|---|---:|---:|
| Universal startup documents | 6 sources | 1 state file; workflow/task docs on demand |
| Routine state owners | 2 (`STATE`, `CURRENT_SPRINT`) | 1 (`CURRENT_STATE`) |
| Routine required document updates | Up to 6+ | 1 |
| Workflow documents | 2 | 1 |
| Active engineering/repository standard files | 4 | 1 |
| Handoff mechanism | Informal archive/chat dependency | 1 repository file |
| Changelog/report cadence | Per meaningful session/mission | Milestone/sprint closure |

## Risks and Controls

- **Risk**: state grows into a diary. **Control**: replace stale facts; history belongs in Git/reports.
- **Risk**: lazy loading misses a constraint. **Control**: task router names required context; ADR links remain discoverable.
- **Risk**: consolidated standards become too large. **Control**: split only when a section has an independent owner/update cadence and repeated use.
- **Risk**: historical docs mention removed v1 paths. **Control**: historical plain-text evidence remains; all navigable Markdown links must resolve.

## Review Plan

After two product sprints, assess the ADR-0006 metrics: touched governance files/session, startup context count, broken links, handoff success, and state size. Refactor only if measured friction returns.
