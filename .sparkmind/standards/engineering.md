# Engineering Standards

> **Version**: 2.0 · **Status**: Active · **Updated**: 2026-07-13
> **Owner**: Engineering

This document owns code, repository, source-structure, dependency, testing, and environment standards.

## Core Rules

- Use TypeScript with `strict: true`; prefer `unknown` + narrowing over `any`.
- Optimize for readable, small, focused code. Apply Rule of Three before abstraction.
- Handle errors explicitly; remove dead code instead of commenting it out.
- Add dependencies only for current requirements; record architecture-impacting choices in an ADR.
- Never commit secrets, local environment files, build output, logs, or temporary files.
- Keep the repository clean: descriptive names, no unexplained files, no empty placeholder directories.

## Monorepo Boundaries

```text
apps/       deployable applications: UI, routing, composition
packages/   reusable code and business/platform logic
docs/       technical setup and architecture
.sparkmind/ governance, current state, decisions, and delivery records
```

- `apps/*` may depend on `packages/*`; packages must not depend on apps.
- Avoid dependency cycles between packages.
- Cross-workspace imports use `@sparkmind/<name>` with `workspace:*`, never relative traversal.
- Create `packages/ui`, `packages/ai`, or `packages/foundry` only when the active sprint needs them.
- A package normally provides `package.json`, `tsconfig.json`, ESLint config, `README.md`, and `src/index.ts`.
- Required scripts: `lint` and `type-check` for all workspaces; `dev`/`build` for deployable apps.

## Current Placement

| Code | Location |
|---|---|
| Next.js pages/layout/routes | `apps/web/src/app/` |
| App-specific components | `apps/web/src/components/` when needed |
| Shared utilities/types | `packages/shared/src/` |
| Future platform logic | `packages/foundry/` |
| Future LLM providers | `packages/ai/` via Vercel AI SDK |

LLM prompts belong with Foundry prompt assets, not hardcoded in UI. Provider failures require explicit timeout/rate-limit handling and a clear fallback.

## Environment Contract

- Root `.env.example` lists every used variable without secret values.
- Local app values live in `apps/web/.env.local` and are gitignored.
- Production values live in the deployment provider's secret store.
- Browser-visible values use `NEXT_PUBLIC_*`; all other names use `SCREAMING_SNAKE_CASE`.
- Add an environment variable only when code uses it; update setup documentation when onboarding changes.
- Centralize runtime configuration after three or more variables justify a config module.

## Verification

For code changes, run the relevant subset—normally all before a milestone:

```bash
pnpm lint
pnpm type-check
pnpm build
pnpm format:check
```

Also run a behavior-level smoke test for the changed flow. Add unit tests for reusable/core logic; do not substitute type-checking for behavioral tests.

For repository review, run:

```bash
git diff --check
git status --short
git diff --stat
```

## Naming

- General files/directories: `kebab-case`, unless a framework requires a convention.
- ADR: `ADR-XXXX-short-title.md`.
- Sprint: `sprint-XXX-short-title.md`.
- Report: `XXX-short-title.md` (multiple reports in one sprint may share the prefix).
- Source files use the framework convention; exported React component names use `PascalCase`.
