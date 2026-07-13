# Sparkmind System Architecture

> **Version**: 2.0 · **Status**: Active · **Updated**: 2026-07-13
> **Owner**: Engineering

This document owns technical architecture. Current delivery status and blockers live in [CURRENT_STATE](../.sparkmind/CURRENT_STATE.md); stack rationale lives in [ADR-0001](../.sparkmind/decisions/ADR-0001-tech-stack-v1.md).

## Target Layers

```text
sparkmind.biz.id
      │
Cloudflare DNS / security / CDN
      │
Vercel: Next.js application and API routes
      ├── Vercel AI SDK provider layer
      └── Supabase data/storage
            ├── Clerk authentication
            ├── Resend email
            └── PostHog/Sentry observability
```

These are target boundaries, not a claim that every service is integrated.

| Layer | Responsibility | Current implementation |
|---|---|---|
| Edge | DNS, WAF, CDN | Not configured |
| App | UI, SSR/SEO, route composition | Next.js placeholder in `apps/web` |
| AI | Provider-neutral LLM access | Not implemented |
| Platform | Reusable Foundry workflows/knowledge | Not implemented |
| Data | Relational data, storage, vector search | Not integrated |
| Identity | User/session/organization identity | Not integrated |
| Observability | Product analytics and errors | Not integrated |

## Monorepo Boundaries

```text
apps/
└── web/            deployable Next.js app
packages/
└── shared/         lightweight shared TypeScript exports
.sparkmind/         engineering operating context and governance
docs/               technical setup and architecture
```

Future `packages/ui`, `packages/ai`, and `packages/foundry` are created only when an approved sprint uses them. Placement and dependency rules are canonical in [Engineering Standards](../.sparkmind/standards/engineering.md#monorepo-boundaries).

## Architectural Principles

1. **Platform first**: vertical products configure Foundry rather than clone a new stack ([ADR-0003](../.sparkmind/decisions/ADR-0003-foundry-platform-first.md)).
2. **Progressive structure**: create modules and infrastructure when requirements exist.
3. **Replaceable boundaries**: provider-specific calls stay behind focused adapters.
4. **Free tier during bootstrap**: paid services require Founder approval ([Constitution](../.sparkmind/CONSTITUTION.md)).
5. **Apps compose; packages own reusable logic**.

## SDOS v2 Architecture

SDOS is a context graph, not a mandatory reading bundle:

```text
CURRENT_STATE
      │
      ├── active sprint
      ├── task-specific standard/doc
      ├── relevant ADR
      └── SESSION_HANDOFF (only if active)
```

The router and ownership map are in [`.sparkmind/README.md`](../.sparkmind/README.md). ADR-0006 records the consolidation and lazy-loading decision.

## Constraints

- No product API, database, auth, or deployment exists yet.
- The web route is a placeholder and does not represent the planned Landing Page.
- CI/CD is deferred until a real delivery need exists.
- Secrets and production infrastructure must never be inferred from target architecture.
