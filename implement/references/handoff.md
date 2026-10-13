# Delivery report and manual QA

Deliver the report in the invoking Codex chat. Use compact prose or bullets, and a small verification table only when it makes several outcomes easier to compare. Scale detail to the change. No separate completion-report file is required.

Include:

- Changed behavior and implementation scope, with artifact pointers where useful.
- Agent-run checks labeled passed, failed, not run, or not applicable, with commands/evidence and meaningful coverage limits. Trace acceptance criteria to evidence or explicit gaps; a passing narrow test does not establish unrelated behavior.
- Requirements and documentation/standards audit conclusions, findings, fixes, and unresolved decisions.
- CodeRabbit command outcome, review coverage, finding dispositions, fixes, revalidation, and any incomplete review or post-review changes.
- Remaining blockers and deferred local issue links.
- A concise manual QA checklist and the overall `awaiting manual QA` status when implementation and required checks are finished. If required implementation gates remain blocked, report that status instead of implying readiness for acceptance.

Derive manual items from agreed requirements, changed behavior, and gaps in agent verification. Each item gives setup or fixture, action, and expected observable result. Select relevant happy paths, failure/recovery, permissions, persistence, retries, or visual behavior; avoid a generic exhaustive checklist. Example shape:

```markdown
- [ ] With <setup>, perform <action>; expect <observable result>.
```

Leave manual checkboxes unchecked until the user reports the checks performed. Agent checks do not stand in for user QA. For multi-phase work, provide the consolidated checklist after the whole plan is implemented, not after each phase. A directly scoped change receives its checklist at delivery.

End the run without actively waiting. Overall completion requires user-confirmed QA. Same-scope defects reopen affected work; after fixes, repeat affected agent checks and manual QA items rather than the whole checklist by default. Keep remaining unchecked acceptance items visible. A disclosed CodeRabbit failure remains visible even when user QA subsequently passes.
