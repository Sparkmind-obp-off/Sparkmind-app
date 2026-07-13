# Development Setup

> **Version**: 2.0 · **Status**: Active · **Updated**: 2026-07-13
> **Owner**: Engineering

## Prerequisites

- Git
- Node.js 20 or newer (`.nvmrc`)
- pnpm 10.13.1 via Corepack (`package.json#packageManager`)

```bash
corepack enable
corepack prepare pnpm@10.13.1 --activate
```

## Clone and Install

```bash
git clone https://github.com/Sparkmind-obp-off/Sparkmind-app.git
cd Sparkmind-app
pnpm install
```

## Environment

The current placeholder app has no required secrets. For future variables:

```bash
cp .env.example apps/web/.env.local
```

Follow the environment contract in [Engineering Standards](../.sparkmind/standards/engineering.md#environment-contract). Never commit `.env.local`.

## Run

```bash
pnpm dev
# or only the web app
pnpm --filter @sparkmind/web dev
```

Open http://localhost:3000.

## Quality Commands

| Command | Purpose |
|---|---|
| `pnpm lint` | ESLint across workspaces |
| `pnpm type-check` | TypeScript checks |
| `pnpm build` | Production build |
| `pnpm format` | Apply Prettier |
| `pnpm format:check` | Verify formatting |

Before a code milestone, run all four checks plus a behavior-level smoke test. Documentation-only changes still require link validation and `git diff --check`.

## Troubleshooting

| Symptom | Action |
|---|---|
| `pnpm` not found | Run the Corepack commands above |
| Wrong Node version | Run `nvm use` or install Node 20+ |
| Workspace links missing | Run `pnpm install` from repository root |
| Restricted network install | Use `pnpm install --network-concurrency=3 --child-concurrency=1` |

Workflow and commit policy: [`.sparkmind/WORKFLOW.md`](../.sparkmind/WORKFLOW.md).
