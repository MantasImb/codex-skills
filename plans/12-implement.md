# Plan: Add implement

Status: draft for a later design session. Target: a new `implement` skill and Codex metadata.
Dependencies: the TDD, adapter, audit, handoff, planning, compatibility, and QA plans in this folder.

## Settled direction

`implement` coordinates delivery using existing skills. It exclusively owns CodeRabbit; TDD will no longer invoke it, even standalone. Keep the skill concise and place specialized policy in references.

## Proposed workflow

1. Load the approved PRD/plan, selected phases, acceptance criteria, agreed test boundaries, relevant domain docs, and ADRs. Reuse prior approvals; resolve material blockers.
2. Record the baseline revision, existing changes, and intended scope so review can distinguish task work from unrelated changes.
3. Implement unblocked phases through the appropriate TDD adapters, one behavior at a time, with refactoring after GREEN.
4. Run repository checks and relevant integration/runtime/browser verification. Record actual outcomes against acceptance criteria.
5. Run `branch-doc-audit` for requirements and standards/documentation drift. Present findings before applying authorized in-scope fixes; surface decisions that change the approved contract.
6. After audit fixes and passing relevant checks, run `cr review --agent`. Move TDD's review policy here: complete triage, reasoned rejection, accepted fixes, affected verification, and one final review after material review-driven changes. Report genuine execution failures.
7. Recheck affected tests and audit conclusions after fixes, update plan status/evidence, and return a concise delivery report plus manual QA checklist.

## Completion contract

- Automated verification and both review surfaces have recorded outcomes; unresolved required gates remain visible.
- Requirements trace to verification evidence or explicit gaps. Human QA remains pending until performed.
- The final report gives changes, checks, audit/CodeRabbit findings and dispositions, limitations, and concrete manual QA steps with expected results.
- Keep standalone skills usable. Proposed default: leave workspace changes reviewable; commits, publication, and parallel integration orchestration require their own scope.

## Acceptance criteria

- [ ] An approved plan runs through TDD, audit, CodeRabbit, and final QA reporting without repeated unchanged approvals.
- [ ] Only `implement` owns the CodeRabbit gate; multiple phases do not cause duplicate per-phase reviews.
- [ ] Review-driven fixes receive appropriate revalidation; blocked checks cannot appear as passes.
- [ ] A later session can resume from recorded phase status, artifacts, and remaining work.

## Questions for the next session

- Require a PRD/plan, or also accept a directly scoped change or bug report?
- Default execution scope: one phase or all approved unblocked phases?
- Keep manual QA as a handoff, or make selected checks completion blockers?
- Require explicit invocation, and what is the completion state when CodeRabbit cannot run?
