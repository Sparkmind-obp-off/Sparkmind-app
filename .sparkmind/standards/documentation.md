# Documentation Standards

> **Version**: 2.0 · **Status**: Active · **Updated**: 2026-07-13
> **Owner**: Engineering

Documentation exists to reduce delivery and recovery cost. If a fact has one canonical owner, every other document links to it instead of copying it.

## Principles

1. **One document, one responsibility.** Use the ownership map in `.sparkmind/README.md`.
2. **Progressive documentation.** Create docs for real systems or recurring needs, not anticipated ones.
3. **Minimal context.** Write skimmable headings, tables, and links so readers can stop early.
4. **Replace stale state.** Living state is current truth, not a chronological diary.
5. **Archive evidence.** Sprint files, reports, and ADRs are historical and should not be startup context.
6. **Executable accuracy.** Commands, paths, and reported checks must match the repository.

## Language and Naming

- Internal governance/docs: Bahasa Indonesia or concise technical English; keep each document internally consistent.
- Source code, code comments, and commit messages: English.
- Use relative links for repository documents.
- Metadata is required for active governance and technical documents: version, status, updated date, and owner. Historical records keep their original metadata.

## Update Triggers

| Document | Update only when |
|---|---|
| `CURRENT_STATE.md` | Operational state changes; review every session |
| `SESSION_HANDOFF.md` | Work is interrupted; clear after resume |
| Root `README.md` | Onboarding, project goal, or primary navigation changes |
| Root `CHANGELOG.md` | A milestone/release completes |
| `DECISION_LOG.md` + ADR | A material decision is accepted/superseded |
| Sprint file | Scope/task/retrospective changes |
| Engineering Report | Sprint/milestone closes |
| Technical docs/package README | Behavior, setup, architecture, or public package usage changes |

An untouched document is correct when its owned fact did not change.

## Anti-Patterns

- Session progress repeated in README, sprint, state, changelog, and report.
- Mandatory loading of all context/ADRs at session start.
- README files that only say where another index lives.
- Empty proposal/document folders created in advance.
- Metadata churn with no content change.
- Documentation that restates source code and becomes stale.
- A completed report edited later only to insert a commit hash; Git history already supplies provenance.

## Link and Ownership Review

For a documentation change:

1. Search references to moved/removed paths.
2. Validate local Markdown links.
3. Confirm every active fact has exactly one owner.
4. Ensure navigation reaches each active document; archives may be reached through their index.
5. Review for copied status, blockers, roadmap, commands, and version claims.
