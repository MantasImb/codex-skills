# Plan progress and resuming

Keep execution evidence in the existing plan, not a separate report or execution log. Add missing progress fields proportionally; preserve existing phase and requirement IDs. Assign stable phase IDs such as `PH-01` when absent without renumbering existing references. Reference PRD decisions instead of duplicating them.

Record the chosen execution mode, baseline and pre-existing changes, source artifacts, and overall status. For each phase retain dependencies, linked requirements (such as `US-01` / `AC-01` when present), agreed verification boundaries, status, concise observed evidence, gaps, blockers, and next work.

Phase status:

- `pending`: work has not started.
- `in progress`: implementation or required verification remains.
- `blocked`: a named dependency, decision, or required check prevents progress.
- `complete`: the phase is implemented and its required agent checks pass, with evidence. This does not claim human acceptance or a completed delivery-level CodeRabbit review.

Only execute phases whose genuine blocking dependencies are satisfied. On resume, inspect current repository state and recorded evidence; do not trust a status label over contrary code or check results. Rerun checks when intervening changes invalidate evidence, rather than repeating every check by default.

When all phases and required agent checks are finished, and CodeRabbit has completed or followed the disclosed failure/skip policy, set the overall plan to `awaiting manual QA`. End the run with the handoff. Set overall `complete` only after the user confirms manual QA passed; retain any disclosed external-review failure separately.

QA revealing an unmet agreed requirement or regression reopens the affected phase as `in progress`, or `blocked` with a reason. Record the finding and set the overall plan back to an implementation status. Fix, revalidate, and return to `awaiting manual QA` with affected acceptance checks. Do not mark unrelated pending phases complete or quietly turn new ideas into current scope.
