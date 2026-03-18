---
name: write-a-prd
description: Create a PRD through user interview, codebase exploration, and module design, then submit it as a GitHub issue. Use when a user wants to write a PRD, create a product requirements document, or plan a new feature.
---

# Write a PRD

## Overview

Drive the feature from vague idea to implementation-ready PRD.

Work in this order unless the task is already far along:
1. Gather the user's full problem statement and any proposed solutions.
2. Inspect the repository to verify assumptions and understand the current system.
3. Interview the user until the important product and technical decisions are resolved or explicitly deferred.
4. Sketch the modules that would be built or changed, with emphasis on deep modules.
5. Write the PRD and submit it as a GitHub issue.

Skip steps that are already complete or unnecessary.

## Operating Rules

- Treat the conversation as a decision tree, not a form.
- Prefer repository evidence over asking the user for facts the codebase can answer.
- Ask one high-value question at a time unless several questions are tightly coupled.
- Push vague answers toward concrete choices, constraints, and tradeoffs.
- Distinguish clearly between facts from the repo, inferences, and open questions.
- Do not include file paths or code snippets in the PRD.

## Workflow

### 1. Gather the Initial Problem

Start by asking the user for a long, detailed description of:
- The problem they want to solve
- Who is affected
- What success looks like
- Constraints, rollout concerns, and deadlines
- Any solution ideas they already have

If they already provided substantial detail, summarize it back and move on.

### 2. Explore the Codebase

Inspect the repository before asking foundational technical questions.

Look for:
- Existing modules that would own the change
- Similar features, flows, or prior art
- Current interfaces, schemas, config, and API boundaries
- Tests that reveal intended behavior
- Docs, ADRs, and tickets that constrain the design

Report:
- What the codebase clearly shows
- What that implies for the feature
- What remains ambiguous

### 3. Interview Relentlessly

Drive toward a shared understanding by resolving the highest-leverage unknowns first.

Cover, as needed:
- User roles and actors
- Entry points and core flows
- Edge cases and failure modes
- Data ownership and source of truth
- State transitions and persistence
- Permissions and security boundaries
- API and schema changes
- Backward compatibility and migrations
- Observability, rollout, and recovery
- Non-goals and out-of-scope requests

Do not dump a questionnaire. Ask only the next question that materially unlocks the plan.

When the user is vague, force precision:
- "Fast" means latency or throughput targets
- "Simple" means fewer moving parts, less operator burden, or less user friction
- "Support retries" means idempotency, deduplication, or resumable workflows

### 4. Design the Module Shape

Once the feature is mostly understood, sketch the major modules to build or modify.

For each module, identify:
- Its responsibility
- Its interface boundary
- Whether it can be made deep: simple public surface, concentrated internal complexity, easy isolated testing
- Key dependencies and data contracts

Actively look for opportunities to extract deep modules instead of spreading logic across shallow layers.

Then confirm with the user:
- Whether the module breakdown matches expectations
- Which modules deserve explicit test coverage
- Whether any behaviors should be validated only through higher-level integration tests

## Output

Write the PRD using this template:

```markdown
## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A LONG, numbered list of user stories. Each user story should be in the format of:

1. As an <actor>, I want a <feature>, so that <benefit>

## Implementation Decisions

A list of implementation decisions that were made. This can include:

- The modules that will be built/modified
- The interfaces of those modules that will be modified
- Technical clarifications from the developer
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Do NOT include specific file paths or code snippets. They may end up being outdated very quickly.

## Testing Decisions

A list of testing decisions that were made. Include:

- A description of what makes a good test (only test external behavior, not implementation details)
- Which modules will be tested
- Prior art for the tests (i.e. similar types of tests in the codebase)

## Out of Scope

A description of the things that are out of scope for this PRD.

## Further Notes

Any further notes about the feature.
```

## Submission

After the PRD is complete:
- Prefer to show the user the final title and PRD body before submission when the scope or wording is still changing.
- If the user asked for direct issue creation and the repository supports it, create a GitHub issue.
- If issue creation is not possible, provide a ready-to-submit issue title and body.

When creating the issue, use a concrete title that names the user-facing capability rather than an implementation detail.

## Good Outcome

The skill is complete when:
- The important decisions are resolved or explicitly deferred
- The module shape is clear enough to guide implementation
- Testing expectations are explicit
- The PRD is detailed enough for implementation and review
- The issue is created, or the exact issue content is ready for submission
