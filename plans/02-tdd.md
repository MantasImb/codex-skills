# Plan: TDD improvements and review ownership

Status: draft. Targets: `tdd/SKILL.md`, `tdd/tests.md`, relevant UI metadata.

## Outcome

TDD owns behavior tests and the red-green-refactor loop. `implement` owns CodeRabbit; standalone TDD no longer invokes it.

## Changes

- Remove CodeRabbit authorization, execution, completion checklist entries, and final-report requirements from TDD. Move that policy to `implement` during the same rollout.
- Add the tautological-test anti-pattern: expected values come from requirements, worked examples, or another independent oracle rather than duplicating the production calculation.
- Add a contrasting example to `tests.md` and an independent-expectation check to the cycle checklist.
- Consume previously agreed public test boundaries; propose and confirm boundaries only when absent or materially changed. State what each boundary catches and misses.
- Preserve vertical slices, observable behavior, minimal GREEN implementation, and refactoring after GREEN.
- End with tests implemented, verification outcomes, and coverage limits; point to `implement` for the complete delivery workflow.

## Acceptance criteria

- [ ] Standalone TDD contains no CodeRabbit gate or promise of external review.
- [ ] Recomputed expected values are identified as weak test evidence.
- [ ] An approved boundary is reused without another approval checkpoint.
- [ ] RED fails for the intended missing behavior, followed by GREEN and relevant regression checks.

## Coordination

Deliver the ownership move with [12: Implement](12-implement.md), so the required review policy has a new home.
