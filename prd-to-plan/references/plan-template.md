# Implementation Plan Template

Adapt this template to the repository and work. Reference decisions in the PRD rather than copying them. Repeat the phase block for each slice; preserve existing phase and requirement IDs on edits.

```markdown
# Plan: <Feature>

Source PRD: <link>
Overall status: pending
Execution mode: not selected (implement settles phase-by-phase or full-plan scope)
Baseline/task delta: not recorded (implement records revision and pre-existing changes at execution start)

## Execution Context

- Decision references: <PRD sections and linked context docs/ADRs/prototype evidence>
- Execution implications: <compatibility constraints, required integrations, or explicit assumptions>
- Final delivery checks: <required broader/integration checks; implement owns audit and external review>
- Coverage gaps/blockers: <explicit remaining limits, or none identified>

## PH-01: <Observable vertical slice>

Status: pending
Depends on: none
Source stories/criteria: <US-01; AC-01 and links>

### What to Build

The narrow end-to-end behavior this phase delivers.

### Acceptance and Planned Verification

- <AC-01 reference and brief observable outcome>
  Method/boundary: <agreed or proposed test/runtime method; relevant existing conventions>
  Proves: <behavior and real collaborators exercised>
  Gaps/additional checks: <remaining verification or none identified>

### Observed Evidence and Next Work

- Checks/results: not run
- Artifacts: none yet
- Blockers/remaining work: <what still needs implementation or verification>

## Final Acceptance

User manual QA: pending; checklist is delivered by implement after the full plan.
User QA confirmation: not received.
External review outcome: not run; implement records completed review or disclosed failure.
```

Initial fields describe planned work, not completed checks. When extending a plan already in progress, retain actual statuses and evidence instead of replacing them with these initial values. Keep manual items unchecked until the user reports completion, even when all phases are implemented.
