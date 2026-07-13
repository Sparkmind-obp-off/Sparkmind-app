# Sparkmind Development Operating System (SDOS) v2

> **Version**: 2.0 · **Status**: STABLE / FROZEN
> **Last updated**: 2026-07-13 (Sprint 001A — Finalization & Freeze)
> **Owner**: Engineering · **Source of truth**: this repository

SDOS is the lightweight operating layer for Sparkmind engineering. It keeps durable context in Git while minimizing what an AI or human must read and update. This file is the canonical AI entry point; a separate `START_HERE.md` would duplicate this responsibility.

## Start in 2 Minutes

1. Read [`CURRENT_STATE.md`](CURRENT_STATE.md): active sprint, current task, blockers, and next action.
2. Read only the task-specific documents from the routing table below.
3. Follow [`WORKFLOW.md`](WORKFLOW.md), implement, verify, update `CURRENT_STATE.md`, commit, and push.
4. If the session stops mid-task, fill [`SESSION_HANDOFF.md`](SESSION_HANDOFF.md).

`CURRENT_STATE.md` is the only document that must be considered at every engineering session. Do not load the whole `.sparkmind/` directory by default.

## Context Router

| Task | Required context | Load only when needed |
|---|---|---|
| Any engineering task | `CURRENT_STATE.md`, `WORKFLOW.md` | Active sprint linked by state |
| Product or business scope | `context/product.md` | `context/company.md`, related ADR |
| Architecture or dependency | `docs/architecture.md`, `DECISION_LOG.md` | Relevant ADR, `context/tech-stack.md` |
| Source code or environment | `standards/engineering.md`, `docs/setup.md` | Package README, architecture |
| Documentation/governance | `standards/documentation.md` | Constitution, related report |
| Resume interrupted work | `SESSION_HANDOFF.md`, `CURRENT_STATE.md` | Files named in handoff |
| Permanent-rule change | `CONSTITUTION.md`, `DECISION_LOG.md` | New ADR required |

## Ownership Map

| Information | Canonical owner | Update trigger |
|---|---|---|
| Active sprint, task, progress, blockers, next action | `CURRENT_STATE.md` | End of a work session or changed state |
| Work lifecycle, Git, handoff policy | `WORKFLOW.md` | Workflow change only |
| Permanent engineering principles | `CONSTITUTION.md` | Founder/CTO approval + ADR |
| Architecture decisions and ADR index | `DECISION_LOG.md` + `decisions/` | Material decision only |
| Business, product, and stack context | `context/` (Founder/CTO) | Strategy or approved stack changes |
| Engineering and repository rules | `standards/engineering.md` | Standard changes |
| Documentation rules and ownership | `standards/documentation.md` | Documentation policy changes |
| Technical architecture | `docs/architecture.md` | Architecture changes |
| Local setup | `docs/setup.md` | Setup/tooling changes |
| Milestone history | root `CHANGELOG.md` | Release or milestone only |
| Sprint plan and retrospective | `sprints/sprint-XXX-*.md` | Sprint planning/closure |
| Evidence and outcomes | `reports/` | Once at sprint closure |
| Interrupted-session recovery | `SESSION_HANDOFF.md` | Only while a handoff is active |

## Structure

```text
.sparkmind/
├── README.md              # navigation and ownership
├── CURRENT_STATE.md       # single operational state
├── SESSION_HANDOFF.md     # temporary recovery context
├── WORKFLOW.md            # session + Git lifecycle
├── CONSTITUTION.md        # permanent rules
├── DECISION_LOG.md        # ADR policy and index
├── context/               # durable business/product/stack knowledge
├── standards/             # engineering and documentation standards
├── decisions/             # append-only ADRs
├── sprints/               # sprint plans and retrospectives
├── reports/               # sprint-level evidence and audit reports
└── templates/             # ADR, sprint, and sprint report templates
```

Historical sprints, reports, and ADRs are archives: they are discoverable through links but are not startup context.

## SDOS v2 Operating Rules

- **One Update Principle**: routine sessions update only `CURRENT_STATE.md`; update other documents only when their owned fact changes.
- **Lazy context**: follow links, never preload every document.
- **Progressive documentation**: create a document only when a real system or recurring need exists.
- **One document, one responsibility**: link to canonical facts instead of copying them.
- **Milestone reporting**: update `CHANGELOG.md` and create an Engineering Report only at milestone/sprint closure.
- **Clean handoff**: `SESSION_HANDOFF.md` is empty by default and temporary when used.
- **Freeze guard**: SDOS v2 is frozen. Reopen its architecture only for measured recurring friction, a significant defect, or a genuinely new governance need; record the reason before changing the operating model.
