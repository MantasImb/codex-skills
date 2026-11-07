---
name: grill-with-docs
description: Run requested interactive discovery for a feature, issue, application, or repository/documentation goal while maintaining domain docs and ADRs. Use when decisions should be challenged and documented against repository evidence; ordinary explanation requests do not start grilling. Development sessions conclude with a PRD unless requested otherwise.
---

# Grill With Docs

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

Run interactive discovery that treats documentation as part of the conversation. Challenge proposals against the repository's existing language and decisions, inspect code before asking factual questions, and update docs when the conversation resolves durable domain terms or architectural choices.

## Session Goal

Start from a referenced issue or a typed goal. Read the referenced issue using available repository files or connected tools; clarify an ambiguous reference. Infer whether the user is preparing development work, understanding the repository, or creating documentation such as a study plan. Ask only when the goal is ambiguous, and follow explicit goal changes during the conversation.

- Development preparation resolves feature, bug, or application decisions and concludes with a PRD.
- Understanding or documentation work concludes with the requested explanation or document; it does not require a PRD.

`grill-me` is also suitable for understanding and documentation sessions. This skill additionally maintains relevant domain docs and ADRs. Do not make every session follow the development pipeline.

## Discovery Mode

Stay in discovery and documentation mode until the user explicitly requests implementation.

Treat answers to design questions as approval of design decisions only. They do not authorize application code changes, test changes, migrations, generated implementation artifacts, or refactors.

Allowed changes during this mode:

- Update `CONTEXT.md` and `CONTEXT-MAP.md` when domain language, boundaries, relationships, or ambiguities are resolved.
- Create or update ADRs when a durable architectural decision meets the ADR criteria.
- Edit planning or documentation artifacts directly tied to the design discussion.
- Record intentionally deferred exploration in the backlog under the policy below.
- Create or update small local issues for actionable unrelated findings under the deferred-issue policy below.

Before modifying application code or tests, require a clear implementation request such as "implement this," "make the code change," "write the tests," or equivalent explicit wording.

## Core Workflow

1. Identify the session goal, source issue when applicable, scope, and current uncertainty.
2. Inspect existing repository docs before asking questions the repo can answer.
3. Build a working decision tree appropriate to that goal. For development, consider constraints, domain terms, boundaries, interfaces, persistence, failure handling, migration, testing, and rollout; avoid imposing irrelevant product decisions on a study or understanding session.
4. Resolve the next blocking branch with one question at a time.
5. Recommend a concrete answer with each question, including the trade-off behind it.
6. Update `CONTEXT.md` immediately when a domain term or relationship becomes clear.
7. Offer an ADR only when the decision is durable, surprising, and trade-off driven.

Do not dump a questionnaire. Ask one focused question, wait for the user's answer, update the working model, then continue.

Reuse settled decisions. Mark unresolved questions as blocking or non-blocking with a reason relative to the intended output. Resolve blockers before presenting that output as ready; record non-blocking assumptions and uncertainties explicitly. Ask again only when new evidence materially changes a decision or an unresolved question blocks progress.

## Discussion Buffer and Direction

Choose the discussion path by dependency and relevance to the goal. Keep a proportional buffer of unresolved topics in chat, including branches discovered during the discussion. An unresolved topic within the current goal stays in this buffer until resolved or intentionally deferred.

Show a concise view of remaining topics at the start based on what is known, after a meaningful subtopic is resolved, and when discoveries materially change the path. Explain what became settled, which topics block the intended output, and why the recommended next topic comes next. Continue with the next focused question without requiring the user to choose a branch. The user can redirect at any point. Do not repeat the buffer after every answer or treat the initial list as exhaustive.

Keep the active buffer in chat; do not create a continuation document or a file mirroring the interview. If the user explicitly requests a handoff to another chat, save remaining exploration in the backlog and concrete problems as local issues, with enough context and links to resume. Preserve settled decisions in their existing artifacts and clearly identify unresolved blockers. A handoff request authorizes this capture, not a claim that the design is complete.

## Repository Discovery

Look for documentation in this order:

- `CONTEXT-MAP.md` at the repository root.
- Root `CONTEXT.md`.
- Context-local `CONTEXT.md` files near the modules affected by the plan.
- Root or context-local `docs/adr/`.
- README, architecture notes, RFCs, issue docs, schemas, tests, and similar features.

If `CONTEXT-MAP.md` exists, treat the repository as multi-context. Use the map to find context-specific glossaries and ADR directories. If there is no map, assume a single root context unless the codebase clearly says otherwise.

Create documentation lazily. Do not create `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/adr/` until the conversation produces content worth recording.

Reuse repository domain-document locations, formats, and naming conventions. Do not rename `CONTEXT.md` to an upstream glossary name solely for parity.

## Domain Language

Challenge terminology as soon as it becomes ambiguous or conflicts with existing docs.

Use this pattern:

```text
Your glossary defines "cancellation" as X, but this plan seems to use it as Y. Should we revise the glossary, rename this concept, or change the plan?
```

When language is fuzzy, propose a canonical term instead of accepting vagueness:

```text
You said "account." I think this should be either "Customer" or "User" because ownership and permissions differ. My recommendation is "Customer" if the concept owns billing state. Which one is correct?
```

Use concrete scenarios to test boundaries, especially lifecycle changes, partial failure, cross-context relationships, ownership, and source-of-truth questions.

## Code Evidence

If a factual answer might exist in the codebase, inspect the code first.

When code and discussion conflict, surface the contradiction directly:

```text
The code cancels entire Orders, but the plan assumes partial cancellation. Should partial cancellation become new behavior, or is the plan using the wrong term?
```

Separate observed facts, inferences, and open questions. Do not let implementation details leak into `CONTEXT.md` unless they name a domain concept that a domain expert would recognize.

## Context Docs

When a domain term, relationship, invariant, or boundary is resolved, update the relevant `CONTEXT.md` during the session instead of batching the work.

Read [context-format.md](references/context-format.md) when writing context docs, adapting its structure to repository conventions. Keep `CONTEXT.md` domain-facing:

- Prefer terms a domain expert would use.
- Pick canonical terms and record ambiguous or rejected aliases as words to avoid.
- Include relationships with cardinality when that helps clarify the model.
- Add a short example dialogue when it clarifies how related terms interact.
- Exclude general programming concepts, implementation details, file paths, framework names, and low-level mechanisms unless they are part of the domain language.
- In multi-context repositories, infer the relevant context from `CONTEXT-MAP.md`; ask when unclear.

## ADRs

Offer an ADR only when all three conditions hold:

- Hard to reverse: changing the decision later would have meaningful cost.
- Surprising without context: a future reader would wonder why the choice was made.
- Trade-off driven: reasonable alternatives existed and the selected path has specific consequences.

Read [adr-format.md](references/adr-format.md) when writing ADRs; preserve existing repository locations, numbering, and format.

Do not create ADRs for obvious choices, easy-to-reverse preferences, or decisions that are better captured as glossary language.

## Backlog and Local Issues

Distinguish deferred exploration from identified problems. An unanswered design question is not automatically an issue.

### Intentional Backlog Deferrals

Use the repository's backlog location and format; otherwise use root `BACKLOG.md`, created only when needed. Capture the deferred topic, why it matters, the unresolved discussion or decision, and relevant context and links. Check for duplicates and update existing entries.

Move exploration from the discussion buffer to the backlog only when the user intentionally defers it or explicitly requests a handoff. You may recommend deferral, but silence, a topic change, or reaching session end is not agreement. A non-blocking deferral needs no additional confirmation once the user's intent is clear.

If a proposed deferral would block the intended output, explain the consequence before finalizing it and prompt the user to confirm or provide context. Recommend a concrete alternative where useful, such as a smaller scope that removes the dependency. Use the response to resolve the dependency, agree on a scope change, or record an intentionally retained blocker. Do not ask again if the user has already acknowledged the consequence and confirmed the deferral. Filing the entry does not remove the blocker or make the output ready.

A backlog entry is not a commitment to implement. Starting to explore it does not remove it: keep it until there is a recorded outcome, then record the resolution or link the resulting artifact, such as a PRD, following repository archival conventions. Link related issues rather than duplicating their content.

### Concrete Local Issues

Capture actionable unrelated bugs or improvements as small local Markdown issues without requesting confirmation for each one. Reuse the repository's issue-folder and naming conventions; otherwise use `issues/` and state the location. Check for duplicates and update an existing issue when appropriate.

Record a title, problem/opportunity, observed evidence or explicit uncertainty, expected behavior when known, reproduction when available, why it is outside the session's scope, and a brief next step. Link captured issues in the recap. Keep them outside the feature PRD's scope unless the user changes that scope. Creating an issue authorizes neither fixing it nor publishing it externally. If a finding blocks current requirements, surface the dependency and a targeted scope decision; filing an issue does not resolve it.

## Conclude the Session

When the user indicates grilling is finished, use the current agreed goal to choose the output. Do not silently stop with a proposed next step when the closing artifact is authorized.

For development preparation:

1. Give a concise chat recap of objective/scope, resolved decisions, assumptions, deferred questions, verification boundaries and limits, backlog and issue links, and any remaining active topics. Name any remaining blockers before claiming readiness. Do not automatically defer unfinished topics merely because the session ends.
2. Unless the user explicitly requests otherwise, resolve the available `to-prd` skill's installed location, read its `SKILL.md`, and follow it immediately to create the PRD from the concluded discussion. Do not assume a Claude `Skill` tool or sibling installation. Do not add another PRD confirmation or reopen settled decisions. If the dependency is unavailable, report that limitation and preserve the recap instead of claiming PRD creation succeeded.
3. Carry scope, resolved feature/application decisions, explicit assumptions, non-blocking deferrals, proposed versus agreed test boundaries, and links to the source issue, domain docs, ADRs, and prototype evidence into the PRD. Keep reusable domain vocabulary/invariants in context docs and significant architecture rationale in ADRs; the PRD references them and owns the feature decisions. Do not create separate approval metadata or a standalone handoff document.

For understanding/documentation, deliver the requested explanation or document plus relevant decisions, uncertainties, remaining active topics, and backlog/issue/document links. Do not invoke `to-prd` merely because the session concludes. If development grilling explicitly skips a PRD, provide the recap and requested output without claiming a durable PRD exists.

The normal development sequence continues with `prd-to-plan`, then explicitly requested `implement`. Creating the PRD does not start planning or implementation automatically. A changed session goal changes the closing output accordingly.
