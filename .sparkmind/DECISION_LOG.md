# Decision Log

> **Version**: 2.0 · **Status**: Active · **Updated**: 2026-07-13
> **Owner**: Engineering

This is the canonical ADR index. Read it only for architecture, dependency, governance, or scope decisions; then open only the relevant ADR.

## ADR Policy

- Create an ADR for a durable decision with meaningful alternatives or consequences—not for routine implementation.
- Use `templates/adr.md` and the next four-digit number.
- ADRs are append-only. A later ADR marks an earlier decision partially/fully superseded; history is not deleted.
- Add the ADR to this index in the same change.

## Index

| ADR | Decision | Status | Area |
|---|---|---|---|
| [ADR-0001](decisions/ADR-0001-tech-stack-v1.md) | Hybrid Vercel + Cloudflare tech stack v1.0 | Accepted | Infrastructure |
| [ADR-0002](decisions/ADR-0002-sdos-structure.md) | Durable knowledge lives in the repository | Partially superseded by ADR-0006 | Governance |
| [ADR-0003](decisions/ADR-0003-foundry-platform-first.md) | Foundry platform-first product architecture | Accepted | Product architecture |
| [ADR-0004](decisions/ADR-0004-sprint-renumbering.md) | Sprint roadmap renumbering | Accepted | Delivery |
| [ADR-0005](decisions/ADR-0005-sprint-002-rescope.md) | Sprint 002 becomes engineering foundation only | Accepted | Delivery |
| [ADR-0006](decisions/ADR-0006-sdos-v2-context-driven-operations.md) | SDOS v2 context-driven, single-state operations | Accepted | Governance |

## Quick Routing

- Hosting, database, framework: ADR-0001.
- Product/platform boundary: ADR-0003.
- Historical sprint numbering/scope: ADR-0004 and ADR-0005.
- Repository context and SDOS operations: ADR-0002 and ADR-0006.
