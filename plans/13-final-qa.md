# Plan: Final verification report and manual QA

Status: draft. Owner: `implement`; use a supporting reference if needed.
Depends on: [01: Workflow handoffs](01-workflow-handoffs.md).

## Outcome

The final handoff states what was verified and gives the user a short checklist for the remaining acceptance checks.

## Changes

- Derive QA items from acceptance criteria, changed behavior, and gaps in automated/runtime verification.
- Each manual item specifies setup or fixture, action, and expected observable result; aim for a few high-value items rather than a generic checklist.
- Report agent-run checks separately as passed, failed, not run, or not applicable, with commands or artifact pointers.
- Cover relevant happy paths, failure/recovery, permissions, retries, persistence, or visual behavior according to the change.
- Keep manual checkboxes unchecked until performed; distinguish implementation progress from final acceptance.
- Include brief audit and CodeRabbit dispositions, material limits, and remaining blockers in the same final report.

## Acceptance criteria

- [ ] Every manual item is executable and has a concrete expected result.
- [ ] The report cannot imply that an unrun check or pending human QA passed.
- [ ] Remaining checks trace to requirements or an explicit verification gap.
- [ ] A simple change receives a proportionately short handoff.

## Open decision

- Use a small verification table or compact prose for agent-run results?
