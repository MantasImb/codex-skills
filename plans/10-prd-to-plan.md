# Plan: Dependencies and verifiable phase progress

Status: draft. Targets: `prd-to-plan/SKILL.md`, plan template and metadata.
Depends on: [01: Workflow handoffs](01-workflow-handoffs.md), [09: To PRD](09-to-prd.md).

## Outcome

A plan shows what can start, what each phase proves, and what remains incomplete.

## Changes

- Give phases stable IDs, genuine blocking dependencies, status, and links to source requirements/test boundaries.
- Record acceptance criteria, verification methods, and space for observed evidence. Unrun checks remain explicit gaps.
- Keep independently verifiable vertical slices and size phases so a fresh session can execute them with artifact pointers.
- Add expand-migrate-contract for broad mechanical changes that cannot land as ordinary vertical slices; make compatibility and final integration verification explicit.
- Reuse approved phases when continuing a plan; review changed dependencies or scope rather than repeating the full approval.
- Keep `./plans/` as the current output convention and allow `implement` to update execution status/evidence.

## Acceptance criteria

- [ ] Dependencies have valid IDs, no cycles, and no unnecessary blockers.
- [ ] A fresh session can select an unblocked phase and identify its verification method.
- [ ] A completed phase links to evidence; incomplete verification is visible.
- [ ] A mechanical migration can preserve compatibility until contraction.

## Open decision

- Final phase statuses and whether evidence belongs inline or in a linked execution log?
