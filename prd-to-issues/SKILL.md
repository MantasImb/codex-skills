---
name: prd-to-issues
description: Break a PRD into independently grabbable GitHub issues using tracer-bullet vertical slices. Use when the user wants to convert a PRD into implementation tickets, create GitHub issues from a PRD, or break down approved product scope into end-to-end work items.
---

# PRD to Issues

Turn an approved PRD into a set of independently grabbable GitHub issues built as thin vertical slices.

Work in this order unless the task is already partially complete:
1. Locate the parent PRD issue.
2. Explore the codebase enough to ground the breakdown in the current architecture.
3. Draft tracer-bullet slices as end-to-end issues.
4. Review the breakdown with the user and iterate until approved.
5. Create the GitHub issues in dependency order.

## Operating Rules

- Treat each issue as a vertical slice through the full system, not a horizontal layer milestone.
- Prefer many thin slices over a few thick ones.
- Make each slice demoable, testable, or otherwise verifiable on its own.
- Mark a slice as `HITL` only when it genuinely requires human interaction such as a decision, review, or design signoff.
- Prefer `AFK` slices whenever the work can be implemented and merged without human intervention.
- Distinguish clearly between facts from the PRD, facts from the repo, and your inferences.
- Do not close or modify the parent PRD issue.
- Do not create child issues until the user approves the breakdown.

## Workflow

### 1. Locate the PRD

Ask the user for the PRD GitHub issue number or URL unless it is already present in the conversation.

If the PRD contents are not already in context, fetch them with:

```bash
gh issue view <number> --comments
```

If GitHub access is unavailable, ask the user to paste the PRD body before proceeding.

### 2. Explore the Codebase

Inspect the repository before drafting issues.

Look for:
- Existing architectural boundaries and ownership lines
- Current routes, APIs, schemas, and data models
- Auth and permission mechanisms
- Adjacent flows or prior art
- Test patterns that reveal intended behavior

Summarize what the repo clearly shows, what it implies, and what remains uncertain.

### 3. Draft Vertical Slices

Break the PRD into thin, end-to-end issues.

Each slice should:
- Deliver a narrow but complete path through schema, backend, frontend, and tests when those layers exist
- Cover a coherent subset of the PRD's user stories
- Be independently verifiable

Avoid horizontal slices such as:
- "build the database layer"
- "add all APIs"
- "implement the UI"

Prefer vertical slices such as:
- "user can submit the first draft through the main happy path"
- "reviewer can approve one submitted item and see the result reflected in the product"

Classify each slice:
- `AFK`: implementable without human interaction
- `HITL`: blocked on a human decision, review, or external approval

### 4. Review the Breakdown with the User

Present the proposed breakdown as a numbered list.

For each slice, show:
- **Title**: short descriptive name
- **Type**: `HITL` or `AFK`
- **Blocked by**: prior slices, if any
- **User stories covered**: user stories or PRD sections addressed

Then ask:
- Does the granularity feel right: too coarse or too fine?
- Are the dependency relationships correct?
- Should any slices be merged or split?
- Are the right slices marked as `HITL` and `AFK`?

Iterate until the user explicitly approves the breakdown.

### 5. Create the GitHub Issues

Create issues in dependency order so blocker references use real issue numbers.

Use `gh issue create` when available. If direct creation is not possible, produce ready-to-submit issue titles and bodies in the same dependency order.

Use this template:

```markdown
## Parent PRD

#<prd-issue-number>

## What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation. Reference specific sections of the parent PRD rather than duplicating content.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Blocked by

None - can start immediately

## User stories addressed

- User story 3
- User story 7
```

When a slice has blockers, replace the `Blocked by` section with one bullet per dependency, for example:

- Blocked by #123
- Blocked by #124

## Good Outcome

The skill is complete when:
- The PRD has been translated into thin, end-to-end issues
- The dependency chain is explicit and accurate
- The user has approved the granularity and slice types
- The child issues have been created, or exact issue drafts are ready for submission
