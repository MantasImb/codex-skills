---
name: to-prd
description: Turn the current conversation context into a PRD and save matching project-native issue files. Use when the user wants to create a PRD from the current context without a discovery interview.
---

# To PRD

Turn the existing conversation context and repository understanding into an implementation-ready PRD, save it in the project's native PRD location, then save a matching issue file in the project's native issues location.

Do not run a discovery interview. Synthesize what is already known from the conversation and codebase. The only default checkpoint is the module and testing checkpoint described below.

The expected triage label for the created PRD issue is `ready-for-agent`; do not add extra triage labels unless the user explicitly asks.

## Process

1. Explore the repository enough to understand the current implementation, domain vocabulary, nearby prior art, tests, docs, ADRs, any project-native PRD or planning directory, and any project-native issues directory. Prefer repo evidence over assumptions, and use the project's domain glossary vocabulary throughout the PRD.
2. Sketch the major modules that would be built or modified. Look for deep modules: simple, stable, testable interfaces that encapsulate substantial behavior and can be tested in isolation.
3. Check with the user that the module breakdown matches expectations and ask which modules should receive explicit tests. Keep this checkpoint short; do not turn it into a broad interview.
4. Write the PRD using the template below.
5. Save the PRD as Markdown in the project's native PRD, product, planning, docs, or issue-spec directory. Reuse the repository's naming convention when one exists. If no clear convention exists, choose the closest durable project documentation location and state the assumption.
6. Save a matching issue as Markdown in the project's native issues folder with the `ready-for-agent` label represented according to local convention. Use a title that names the user-facing capability, not an implementation detail, and reference the saved PRD file.

When choosing the issue path, prefer the most specific project-native location:

- If the feature belongs to a service or package with its own issues folder, save the issue there.
- If the repository has a shared product or planning issues folder and the feature is cross-cutting, save the issue there.
- Do not create or use a root-level issues folder merely for convenience when the issue naturally belongs inside a service directory.
- If no clear issue-folder convention exists, choose the closest durable project documentation location and state the assumption.

If saving the PRD or issue file is blocked, provide the exact intended path and body.

## PRD Rules

- Write from the user's perspective.
- Be concrete about product behavior, system interactions, and constraints that are known.
- Distinguish repo facts, conversation facts, and explicit assumptions when needed.
- Do not include specific file paths in the PRD.
- Do not include code snippets unless a prototype produced a compact snippet that records a decision more precisely than prose, such as a state machine, reducer, schema, or type shape. If included, trim it to the decision-rich part and note that it came from a prototype.
- Make user stories extensive enough to cover happy paths, edge cases, permissions, errors, state transitions, and operational concerns.
- Testing decisions should favor external behavior over implementation details.

## PRD Template

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

Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it within the relevant decision and note briefly that it came from a prototype. Trim to the decision-rich parts -- not a working demo, just the important bits.

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

## Good Outcome

The skill is complete when:

- The repository context has been inspected or already exists in the conversation.
- The user has confirmed the module and testing breakdown.
- The PRD is detailed enough to guide implementation.
- The PRD is saved in the project's native PRD or documentation location.
- The matching issue file is saved in the most specific project-native issues location with the `ready-for-agent` label, or exact manual issue content has been provided because saving was blocked.
