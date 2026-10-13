---
name: to-prd
description: Synthesize an existing discussion into a local PRD with stable requirements, agreed verification boundaries, and a matching project-native issue. Use when the user requests a PRD from current context or development grilling hands off a concluded discussion; do not restart discovery.
---

# To PRD

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

Turn settled conversation context and repository evidence into a PRD suitable for planning. The PRD owns feature/application requirements, scope, resolved decisions, assumptions, and explicit deferrals. Save it locally and create or update a matching local issue using repository conventions.

## Consume Existing Decisions

Read the concluded discussion, source issue, and existing PRD when available. Inspect only the repository evidence needed to ground missing facts: domain docs, ADRs, relevant code/tests, similar behavior, prototypes, and artifact conventions. Reuse context already gathered instead of repeating discovery.

Carry forward settled module/interface ownership, behavior priorities, and public test boundaries without another confirmation. Ask a short, targeted question only when a missing or materially changed decision blocks the PRD. Distinguish observed facts, agreed decisions, inferences, proposed choices, and explicit assumptions; do not present a new inference as user agreement.

Classify unresolved questions as blocking or non-blocking, with the reason. Resolve blockers before presenting the PRD as ready for implementation planning. If the user requests a draft with blockers, preserve them visibly and do not label its issue ready. Non-blocking unknowns may be explicitly deferred.

## Requirements and Verification

Write from the user's perspective and scale detail to the work. A small bug/change can have a short PRD; a whole application needs enough detail to define its behavior and boundaries. Include relevant happy paths, failures, permissions, state transitions, and operational constraints without imposing a long story list or irrelevant sections.

- Give user stories stable IDs such as `US-01` and acceptance criteria separate IDs such as `AC-01`. Link criteria to their relevant stories where useful. Acceptance criteria describe concrete observable outcomes, not internal implementation tasks.
- Preserve existing IDs when editing; append new IDs without renumbering and never reuse retired IDs. When revising older unlabelled requirements, assign IDs once and retain any existing references. Preserve removed criteria as explicitly retired or record their retirement when needed to keep downstream references understandable.
- Link each criterion to an agreed or proposed verification method, public boundary, and any coverage gap. Prefer a suitable existing higher boundary when it meaningfully proves behavior. Do not choose tests solely by listing modules.
- State what each boundary proves and misses: a service test may not prove real persistence, a DOM test may not prove browser navigation, and a mocked framework call may not prove the runtime effect. Name additional automated/runtime/manual verification where needed, or mark the method as an unresolved proposal/gap.
- Retain durable module ownership, interfaces, schemas, and architecture decisions when they were made. Do not invent a detailed implementation design simply to fill a template.

Keep reusable domain language and invariants in context docs and significant architectural rationale in ADRs. Reference those documents and record their implications for this feature. Reference prototype evidence with its question, evaluated verdict or pending status, and limitations; provisional findings are not settled requirements.

Avoid volatile implementation file paths and helper names in product requirements. Links to source issues, domain docs, ADRs, prototypes, and other durable decision evidence are appropriate. Include a compact prototype-derived model excerpt only when it expresses a decision more precisely than prose; attribute it and omit the runnable demo.

## Save the PRD and Matching Issue

Read [prd-template.md](references/prd-template.md) when drafting. Adapt it to repository templates while retaining requirement IDs, scope, decisions, assumptions/deferrals, evidence links, and verification boundaries. Do not require a separate handoff document or approval metadata.

Reuse the project's native PRD/product/planning/docs/issue-spec location and naming. If no convention exists, choose a durable project documentation location and state the assumption. Update an existing PRD for the same scope rather than creating an unnecessary duplicate.

For the matching local Markdown issue:

- Prefer an existing issue for this work, including the source issue when it represents the same scope. Check for duplicates before creating one, preserving useful evidence and metadata when updating.
- Use the most specific existing issue convention: service/package issues for local features, shared product/planning issues for cross-cutting work. If none exists, use `issues/` and state the location.
- Give it a user-facing title and link the saved PRD. Represent `ready-for-agent` according to local convention when the PRD is ready; do not add other triage labels without a request. Preserve an explicit draft/blocker state when readiness is not established.
- Keep unrelated deferred issues outside the PRD's feature scope, linking them where useful. A current requirement blocker cannot be resolved by merely filing a deferred issue.

Creation or updating here is local documentation work; it does not authorize external publication, commits, or implementation. If saving is blocked, report the exact intended paths and content rather than claiming success.

## Finish

Return concise links to the PRD and matching issue, with any material assumptions, blockers, or verification gaps. A good outcome preserves settled decisions, gives each required behavior observable criteria and a verification method or explicit gap, and remains proportional to the work.

The next development stage is `prd-to-plan`, followed by explicitly requested `implement`. Do not automatically start either merely because the PRD was saved.
