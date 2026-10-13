# PRD Template

Adapt this outline to the repository and scope; do not pad a small change to fill every section. Requirement checkboxes, if used, describe work to be verified later, not checks performed during PRD creation.

```markdown
# PRD: <User-facing capability>

Source issue: <link when present>

## Problem and Outcome

Who needs what behavior, why it matters, and the intended outcome.

## Scope

Included behavior and explicit exclusions. Link unrelated deferred issues when useful.

## User Stories

- **US-01**: As <actor>, I want <capability>, so that <benefit>.

## Acceptance Criteria

- **AC-01** (US-01): Given <setup>, when <action>, then <observable result>.

## Resolved Decisions

Durable choices, ownership/interfaces, constraints, and their implications.
Reference relevant context docs, ADRs, and prototype evidence rather than copying their contents.

## Assumptions and Deferrals

Explicit assumptions, non-blocking unanswered questions and reasons for deferral.
If this is a draft, name remaining blockers and their impact.

## Verification Boundaries

- **AC-01**: <method and public boundary; agreed or proposed>.
  Proves: <behavior/collaborators exercised>.
  Limits/additional verification: <coverage gaps or required runtime/manual checks>.
  Prior art: <relevant repository test convention when useful>.
```

A verification method may cover several criteria; reference each relevant ID rather than duplicating the same description. Preserve story and criterion IDs across revisions, keeping retired IDs understandable for plans and audit references.
