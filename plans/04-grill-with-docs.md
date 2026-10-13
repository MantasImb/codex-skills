# Plan: Grill with docs handoff

Status: draft. Targets: `grill-with-docs/SKILL.md`, supporting references and metadata as needed.
Depends on: [01: Workflow handoffs](01-workflow-handoffs.md).

## Outcome

Discovery ends with a durable, concise record that `to-prd` can consume directly.

## Changes

- Add a closing handoff: objective/scope, resolved decisions, assumptions, deferred questions, proposed or agreed test boundaries, and pointers to domain docs, ADRs, and prototype evidence.
- Mark unresolved questions as blocking or non-blocking, with the reason.
- Record which decisions the user approved so later skills can reuse them.
- Preserve repository-first investigation, one focused question at a time, immediate domain documentation, and sparing ADR creation.
- Preserve discovery-only authorization: design answers do not start application or test implementation.
- Reuse the repository's domain-document conventions; do not rename `CONTEXT.md` to the upstream glossary naming solely for parity.

## Acceptance criteria

- [ ] A fresh session can identify settled decisions and remaining blockers from the saved handoff.
- [ ] `to-prd` can synthesize the discussion without reopening settled questions.
- [ ] Grilling updates documentation while respecting discovery-only scope.

## Open decision

- Which existing artifact should receive the closing handoff when no draft PRD exists?
