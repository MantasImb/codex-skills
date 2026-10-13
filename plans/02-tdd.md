# Plan: TDD improvements and review ownership

Status: draft. Targets: `tdd/SKILL.md`, `tdd/tests.md`, relevant UI metadata.

## Outcome

TDD owns behavior tests and the red-green-refactor loop. `implement` owns CodeRabbit; standalone TDD no longer invokes it.

## Changes

- Remove CodeRabbit authorization, execution, completion checklist entries, and final-report requirements from TDD. Move that policy to `implement` during the same rollout.
- Add the tautological-test anti-pattern: expected values come from requirements, worked examples, or another independent oracle rather than duplicating the production calculation.
- Add a contrasting example to `tests.md` and an independent-expectation check to the cycle checklist.
- Consume previously agreed interfaces, behavior priorities, and public test boundaries from the PRD and implementation plan without repeating settled questions. State what each boundary catches and misses.
- For standalone TDD without a PRD or plan, inspect repository conventions and choose routine testing details autonomously. Ask only when intended behavior or a consequential interface decision is unclear; surface conflicts with recorded decisions before proceeding with affected work.
- Preserve vertical slices, observable behavior, minimal GREEN implementation, and refactoring after GREEN.
- End with tests implemented, verification outcomes, and coverage limits; point to `implement` for the complete delivery workflow.

## Acceptance criteria

- [ ] Standalone TDD contains no CodeRabbit gate or promise of external review.
- [ ] Recomputed expected values are identified as weak test evidence.
- [ ] A previously agreed boundary is reused without another approval checkpoint.
- [ ] Standalone TDD can proceed without a PRD or plan when behavior is clear; routine testing choices do not require confirmation.
- [ ] Unclear behavior or consequential interface decisions trigger a targeted question.
- [ ] RED fails for the intended missing behavior, followed by GREEN and relevant regression checks.

## Coordination

Deliver the ownership move with [12: Implement](12-implement.md), so the required review policy has a new home.
