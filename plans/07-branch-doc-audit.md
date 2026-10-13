# Plan: Requirements-aware branch audit

Status: draft. Targets: `branch-doc-audit/SKILL.md`, metadata and optional report reference.
Depends on: [01: Workflow handoffs](01-workflow-handoffs.md).

## Outcome

Review the intended change against both requirements and repository expectations, with evidence for each finding.

## Changes

- Accept the source PRD/plan and approved acceptance criteria as explicit inputs; report requirements coverage separately from standards/documentation drift.
- Check for missing/partial requirements, incorrect behavior, scope creep, and unverified acceptance criteria.
- Pin the baseline revision and change scope. Account for relevant commits, staged/unstaged work, and new files; distinguish pre-existing changes from task changes.
- Prefer an explicit scope or the baseline recorded by `implement`; investigate a base only when absent and clarify genuine ambiguity.
- Preserve existing drift classifications, facts versus inferences, and report-before-fixes behavior.
- Keep standalone audit read-only unless fixes are authorized. Under `implement`, report first, then let the coordinator fix in-scope findings.
- Keep agent use proportionate and supported; preserve separate requirement and standards conclusions when aggregating.
- Recheck affected audit conclusions after material fixes; report unavailable specs/docs as coverage gaps.

## Acceptance criteria

- [ ] Standards-compliant code that misses a requirement produces a requirements finding.
- [ ] Uncommitted work and relevant new files are included in the declared scope.
- [ ] Stale docs and implementation defects receive different recommended fixes.
- [ ] A clean audit identifies its evidence and any unreviewed surfaces.
