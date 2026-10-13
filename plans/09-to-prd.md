# Plan: PRD test boundaries and traceability

Status: draft. Targets: `to-prd/SKILL.md`, metadata and template references as needed.
Depends on: [01: Workflow handoffs](01-workflow-handoffs.md).

## Outcome

The PRD records observable requirements and agreed verification boundaries, ready for planning and implementation.

## Changes

- Consume the discovery handoff and reuse existing approvals; preserve synthesis rather than restarting discovery.
- Keep module ownership decisions, but replace module-by-module test selection with public boundaries that prove the required behavior.
- Prefer suitable existing higher boundaries; describe what each proves and what needs additional verification.
- Give requirements/acceptance criteria stable identifiers and link testing decisions to them.
- Record assumptions, explicit deferrals, and relevant ADR/prototype pointers without embedding volatile implementation paths in product requirements.
- Keep project-native PRD and issue locations; update completion criteria to recognize prior approval.

## Acceptance criteria

- [ ] Previously approved boundaries are carried forward without another checkpoint.
- [ ] Each required behavior has a verification method or a clearly marked gap.
- [ ] A missing or materially changed boundary produces a short, targeted question.
- [ ] The PRD and matching issue remain usable through project-native conventions.

## Open decision

- Give acceptance criteria their own identifiers or use numbered user stories plus local criteria IDs?
