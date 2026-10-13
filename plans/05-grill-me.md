# Plan: Dependency-aware grilling

Status: draft. Targets: `grill-me/SKILL.md`, metadata if needed.
Depends on: [01: Workflow handoffs](01-workflow-handoffs.md).

## Outcome

Questions resolve the decisions that unlock progress, while keeping the interview easy to answer.

## Changes

- Track prerequisites and ask from the current set of unblocked decisions.
- Keep one focused question as the default; optionally group a few independent questions when useful. Dependent questions wait for their prerequisite answers.
- Give a recommendation and trade-off for each decision question.
- Investigate repository facts directly; use a narrowly scoped agent only when authorized and useful for an unresolved branch.
- Save a closing handoff with settled decisions, assumptions, and explicit deferrals.
- Describe agent lifecycle in terms supported by the current runtime rather than promising a nonexistent close operation.

## Acceptance criteria

- [ ] A dependent question is deferred until its parent decision is settled.
- [ ] Independent questions can be grouped without forcing a large questionnaire.
- [ ] Repo-answerable facts do not become questions for the user.
- [ ] The interview can finish with explicitly deferred, non-blocking unknowns.

## Open decision

- Offer question batching only on request, or let the agent choose for small independent sets?
