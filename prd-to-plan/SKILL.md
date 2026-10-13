---
name: prd-to-plan
description: Translate a PRD into a reviewed local implementation plan with verifiable vertical phases, stable IDs, dependencies, and progress/evidence fields. Use when the user requests implementation planning from a PRD; saving the plan does not start implementation.
---

# PRD to Plan

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

Translate the PRD into independently verifiable phases and save the reviewed plan in `./plans/`. The PRD owns requirements and design decisions; the plan owns sequencing, dependencies, implementation progress, and verification evidence.

## Ground the Plan

Find the supplied PRD in conversation or local files and read its requirements, acceptance criteria, assumptions, deferrals, agreed test boundaries, and linked context docs/ADRs/prototypes. If the source is missing or ambiguous, ask for the specific missing reference. Do not restart settled discovery or invent requirements to fill gaps.

Inspect relevant repository architecture, interfaces, persistence, permissions, integrations, tests, and similar features. Distinguish observed facts from requirements and planning inferences. Resolve material blockers with targeted questions; keep non-blocking assumptions and gaps visible.

Reference durable decisions from the PRD rather than keeping a second copy that can drift. Explain any execution implications, such as a compatibility period or an integration dependency. If repository evidence requires a changed requirement or architecture choice, surface that decision and update the PRD before planning affected work.

## Build Verifiable Phases

Default to thin vertical slices. Each phase delivers a coherent observable path through the layers involved, with enough verification to establish that phase's behavior. Do not impose frontend/backend/database layers when they are irrelevant, or turn every layer into a separate milestone.

For each phase:

- Assign a stable ID such as `PH-01`. Preserve existing IDs across edits; add new IDs without renumbering or reusing retired ones. Keep retired phase references understandable when a phase is removed.
- Reference covered PRD stories/criteria, such as `US-01` and `AC-01`, without assigning new IDs to existing requirements. Use existing source anchors when an older PRD has no IDs; do not silently relabel it only inside the plan.
- Record only genuine blocking phase dependencies, by ID, with a brief reason when not obvious. Independent work should not acquire a dependency merely because it appears later in the document.
- State the behavior to build, acceptance-criterion references, agreed public test boundary, planned verification methods, and remaining coverage gaps. Distinguish phase checks from final delivery checks and user manual QA.
- Leave room for concise observed evidence, blockers, and next work inline. New work starts `pending`; planned tests are not results.

Check that dependency IDs exist, dependencies have no cycles or self-references, and every in-scope acceptance criterion is covered by one or more phases and a verification method or explicit gap. Flag requirements excluded by a user-selected partial scope. Size phases so a fresh session can recover the goal and verification method from the plan and linked artifacts.

Avoid volatile helper names and detailed file-by-file task lists. Artifact pointers and useful existing test conventions are appropriate; they help execution without becoming a second product specification.

## Mechanical Migration Exception

For broad mechanical changes that cannot land as ordinary vertical slices, use expand–migrate–contract:

1. Expand with the compatible new path and verify coexistence with existing callers/data.
2. Migrate callers/data in verifiable increments, stating the compatibility contract and evidence required before removal.
3. Contract only after migration dependencies are satisfied; remove the old path and verify final integration and compatibility expectations.

Explain why this structure fits the change. Include applicable failure/recovery or rollback constraints, and the final verification that proves the migration is complete. Do not use the exception to justify arbitrary layer-first feature plans.

## Review and Save

Present proposed phase IDs, titles, covered requirements, dependencies, and what each phase proves. Review the initial breakdown with the user and iterate on material granularity or scope choices before saving the final plan. A draft, if requested, must be labeled as such.

When continuing or editing an existing reviewed plan, reuse its settled phases and decisions. Review only material changes to scope, dependencies, or phase structure; do not require the whole plan to be approved again. Preserve observed evidence and progress rather than resetting the plan during an edit.

Read [plan-template.md](references/plan-template.md) when writing. Use a feature-appropriate name in `./plans/`, reuse an existing matching plan, and keep its source PRD link valid. No separate handoff file, approval metadata, or execution log is required.

## Progress Contract

The initial plan records an overall implementation status and each phase's status. Use `pending`, `in progress`, `blocked`, and `complete` for phase implementation progress. A completed phase needs passing required agent checks and observed evidence; it does not imply user acceptance or a completed delivery-level external review. Required implementation checks that fail or cannot run prevent phase completion.

The `implement` skill updates status and evidence in place and owns the execution lifecycle. After all phases and required agent checks finish, with external review completed or its disclosed failure handled under `implement`'s skip policy, the overall plan becomes `awaiting manual QA`. It reaches `complete` only after the user confirms QA passed. The implementation run may end while QA is pending.

An unmet agreed requirement or regression found during QA reopens the affected phase as `in progress` or `blocked`, with the finding and revalidation evidence recorded. After fixes, return to `awaiting manual QA` for affected checks. Unrelated enhancements become deferred issues rather than silently expanding the plan. Manual QA is consolidated at the end of the full plan, not repeated after every phase.

## Finish

Return the saved plan link and any material blockers or coverage gaps. Planning is finished when the breakdown is reviewed, dependencies and requirement coverage are coherent, and the file is saved with honest initial progress fields. That does not mean implementation is complete. Do not automatically invoke `implement` or start code/tests merely because the plan exists.
