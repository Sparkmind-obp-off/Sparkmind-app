# Engineering Workflow

> **Version**: 2.0 · **Status**: Active · **Updated**: 2026-07-13
> **Owner**: Engineering

This is the single workflow for AI and human engineers. It replaces the separate session-lifecycle and Git workflow documents.

## 1. Resume or Start

1. Sync `main` and inspect `git status`.
2. If `SESSION_HANDOFF.md` has an active handoff, read it first.
3. Read `CURRENT_STATE.md`.
4. Use the context router in `.sparkmind/README.md`; load only documents relevant to the task.
5. Confirm scope and acceptance criteria. Put unclear business decisions in the blocker table and ask the owner—do not invent scope.

## 2. Plan and Implement

1. Inspect the affected code/docs before editing.
2. Plan the smallest complete change.
3. Follow `standards/engineering.md` and task-specific documentation.
4. Test the changed behavior; never claim unexecuted verification.
5. Avoid speculative files, dependencies, abstractions, and documentation.

## 3. Review

1. Review the complete diff as an external reviewer.
2. Run the relevant quality checks from `docs/setup.md`.
3. Check Markdown links when documentation changes.
4. Confirm no secrets, generated artifacts, temporary files, or accidental changes.

## 4. Update by Trigger

Routine sessions update **only** `CURRENT_STATE.md`. Update another document only if its owned fact changed:

- `DECISION_LOG.md` + ADR: material architecture/governance decision.
- Sprint file: sprint scope, task status, or retrospective changed.
- Root `CHANGELOG.md`: release or milestone completed.
- Engineering Report: sprint/milestone closes, not every session.
- `docs/` or package README: behavior/setup/architecture changed.
- `SESSION_HANDOFF.md`: session stops before the task is safely complete.

Never copy status, roadmap, or blockers into multiple documents.

## 5. Commit and Push

Use atomic Conventional Commits:

```text
<type>(<optional-scope>): <imperative summary>
```

Common types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`. SDOS changes use `docs(sdos)` or `refactor(sdos)`.

Before commit:

```bash
git status --short
git diff --check
git diff --stat
```

Commit to `main` during the bootstrap phase after self-review, then push to `origin main`. Never commit secrets or force-push without an explicitly recorded reason.

## 6. Handoff Protocol

Use `SESSION_HANDOFF.md` only when work is interrupted and cannot be completed safely:

1. Commit and push stable work when possible.
2. Record exact progress, modified files, verification, issues, and one executable next action.
3. Update `CURRENT_STATE.md` to point to the handoff.
4. The next session resumes from the handoff and clears it after completion.

## Definition of Done

- Acceptance criteria met.
- Relevant checks passed and evidence is accurate.
- Canonical documentation updated by trigger.
- No unresolved accidental changes or secrets.
- `CURRENT_STATE.md` has a truthful next action.
- Changes are committed and pushed, unless an active handoff documents why not.
