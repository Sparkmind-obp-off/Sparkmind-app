# Sparkmind

> Building AI Employees for modern businesses.

Sparkmind is a pre-product TypeScript monorepo for the Foundry platform and vertical AI products such as ClinicFlow AI. The repository also contains SDOS v2, its context-driven engineering operating system.

## Status and URLs

- **Phase**: Pre-product; engineering foundation complete
- **SDOS**: Sparkmind Development Operating System v2.0 — STABLE / FROZEN
- **Repository**: https://github.com/Sparkmind-obp-off/Sparkmind-app
- **Planned website**: https://sparkmind.biz.id (not deployed)
- **Current work/blockers**: [`.sparkmind/CURRENT_STATE.md`](.sparkmind/CURRENT_STATE.md)

## Start Here

| Need | Read |
|---|---|
| AI/human engineering session | [SDOS v2 quick start](.sparkmind/README.md) |
| Current task, blockers, next action | [`CURRENT_STATE.md`](.sparkmind/CURRENT_STATE.md) |
| Install and run locally | [`docs/setup.md`](docs/setup.md) |
| Technical architecture | [`docs/architecture.md`](docs/architecture.md) |
| Accepted decisions | [Decision Log](.sparkmind/DECISION_LOG.md) |
| Product direction | [`context/product.md`](.sparkmind/context/product.md) |

## Completed Features

- pnpm + Turborepo workspace.
- `apps/web`: Next.js 15 App Router placeholder application.
- `packages/shared`: shared TypeScript constants and result type.
- TypeScript strict mode, ESLint, Prettier, and workspace scripts.
- SDOS v2 (stable/frozen): canonical AI entry point, minimal context router, single operational state, one workflow, resumable handoff, ADR and sprint governance.

## Functional Entry Points

| Path/command | Purpose | Parameters |
|---|---|---|
| `apps/web/src/app/page.tsx` / `/` | Current placeholder web page | None |
| `pnpm dev` | Start all development workspaces | None |
| `pnpm build` | Build deployable workspaces | None |
| `pnpm lint` | Run workspace linting | None |
| `pnpm type-check` | Run TypeScript checks | None |

No public API routes, authentication flows, or product data endpoints exist yet.

## Data Architecture

- **Data models**: no business/domain models yet; `packages/shared` contains only foundational shared types.
- **Storage**: no database, object storage, or persistent service is integrated.
- **Data flow**: the current web application renders a static placeholder; target architecture is documented in [`docs/architecture.md`](docs/architecture.md).

## Not Yet Implemented

- Production landing page and Book a Demo flow.
- DNS configuration and deployment.
- Foundry AI/provider abstraction and knowledge layer.
- ClinicFlow AI vertical product.
- Authentication, API, database, analytics, and email integrations.
- Automated CI/CD.

## Recommended Next Steps

1. Founder selects the next sprint: Landing Page or Foundry Core.
2. If Landing Page is selected, provide deployment/DNS credentials through secure channels.
3. Implement only the approved sprint and add infrastructure progressively.
4. Measure SDOS v2 after two product sprints; reopen its frozen architecture only if evidence shows significant friction.

## User Guide

```bash
git clone https://github.com/Sparkmind-obp-off/Sparkmind-app.git
cd Sparkmind-app
corepack enable
pnpm install
pnpm dev
```

Open http://localhost:3000. See [`docs/setup.md`](docs/setup.md) for checks and troubleshooting.

## Deployment

- **Target platform**: Vercel application hosting behind Cloudflare DNS/CDN (ADR-0001).
- **Status**: inactive; no production deployment or credentials are configured.
- **Configuration**: deployment details will be added only when the Landing Page sprint is approved.

## License

Proprietary — © 2026 Sparkmind.
