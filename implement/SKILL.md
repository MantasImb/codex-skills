---
name: implement
description: Coordinate explicitly requested implementation of a reviewed plan, scoped bug, or small change through TDD, requirements and documentation audit, CodeRabbit review, and a final manual QA handoff.
---

# Implement

Own delivery in the invoking Codex chat. Start only when explicitly requested. Continue the same scope for later bug fixes, QA findings, or review follow-ups in that chat without requiring another invocation. Unrelated work or another chat needs its own implementation request.

The normal development flow is `grill-with-docs` → `to-prd` → `prd-to-plan` → `implement`. Creating a PRD or plan does not start this workflow. Leave changes reviewable in the workspace; do not automatically commit, publish, schedule work, or orchestrate parallel integration.

## Establish scope

- Load the existing reviewed plan, source PRD, acceptance criteria, agreed test boundaries, relevant `CONTEXT.md`, ADRs, and repository instructions. The PRD owns requirements and decisions; the plan owns execution and evidence. Reuse settled decisions. Ask only about material changes or unresolved blockers, then update the affected artifacts.
- If a PRD exists but no usable implementation plan exists, load `prd-to-plan`, create and review the phases with the user, then settle execution scope. This is a fallback; never regenerate a usable plan or repeat an unchanged phase review.
- A clearly scoped bug or small change can proceed without a PRD or plan. Establish intended behavior from the request and repository evidence. Reproduce a bug's reported symptom and add a failing regression test before fixing it where feasible; disclose reproduction or testing gaps. Larger work or unresolved product decisions needs discovery/planning before affected implementation.
- For a multi-phase plan with no execution mode specified, ask once whether to execute phase by phase or the whole plan. Default to one phase if no preference is supplied. Honor explicit scope and reuse the chosen mode. Phase-by-phase delivery pauses after each phase for user inspection and direction; full-plan delivery proceeds through unblocked dependencies until finished or a decision blocks progress.
- Record the baseline revision, pre-existing staged/unstaged changes and untracked files, intended task scope, and execution mode in the plan. Without a plan, retain this information in chat. Preserve unrelated work and distinguish task changes from pre-existing changes in shared files. Resolve genuine scope ambiguity before auditing.

## Execute and verify

Resolve dependent skills using their available installed locations and read their authoritative `SKILL.md` files. Do not assume sibling directories or a Claude `Skill` tool. If a required dependency is missing, report the concrete limitation instead of claiming that stage ran.

1. Select an unblocked phase within the requested scope. Read [progress.md](references/progress.md) when executing or resuming a plan; update its status and evidence in place.
2. Load `tdd` and the applicable adapter (`tdd-typescript`, `tdd-nextjs-jest`, or `tdd-rust-backend`). Follow one behavior at a time: intended RED failure → minimal GREEN → refactor after GREEN. Reuse agreed interfaces and boundaries. Choose a boundary that proves the requirement; supplement isolated tests with real integration, runtime, or browser checks when required behavior crosses that boundary. Derive expected results independently of the production calculation.
3. Discover verification commands from repository conventions. Run focused checks during implementation and required broader checks at meaningful integration points and at the end. Record commands, outcomes, acceptance-criterion coverage, and gaps. Mocked or isolated tests do not prove an untested runtime flow. Failed or unavailable required implementation checks remain blockers.
4. Load `branch-doc-audit` with the recorded baseline, task delta (including new files), PRD/plan criteria, and relevant docs. Obtain separate requirements-coverage and standards/documentation conclusions. Present findings before repairs, then fix clear in-scope defects without another approval checkpoint. Changes to agreed requirements or conflicting guidance need a targeted user decision. Revalidate affected checks and audit conclusions after repairs.
5. For an intermediate phase, report completed behavior, checks, audit findings, remaining phases, and blockers, then honor execution mode. Do not run a separate CodeRabbit review or repeat final manual QA after every phase.
6. When the full plan or directly scoped change is implemented and relevant checks pass, read [review.md](references/review.md) and run the CodeRabbit gate once for the delivery. Triage findings, fix accepted in-scope problems, and recheck affected tests and audit conclusions. This skill exclusively owns that gate; TDD does not run it.
7. Read [handoff.md](references/handoff.md) and deliver one concise report and consolidated manual QA checklist in chat. Record overall status as `awaiting manual QA` until the user confirms QA passed. The run may end while QA is pending.

## Findings and continuation

Capture actionable out-of-scope findings as small local Markdown issues. Reuse repository issue-folder and naming conventions; otherwise use `issues/` and state the location. Check for duplicates and update an existing issue when appropriate. Record title, problem/opportunity, evidence or uncertainty, expected behavior when known, reproduction when available, why deferred, and a brief next step. Link these issues in the report. Issue creation authorizes neither a fix nor external publication. A finding blocking current requirements stays a blocker; filing an issue does not resolve it.

For QA defects or regressions in the agreed scope, reopen affected work and continue this workflow. After fixes, rerun affected verification and present the affected manual QA items. New feature ideas become deferred issues. A user-requested later CodeRabbit review uses the same review policy without reinvocation or automatic scheduling.
