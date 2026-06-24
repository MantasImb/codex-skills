---
name: grill-with-docs
description: Interactive plan grilling that stress-tests a proposal against repository docs, domain language, code evidence, CONTEXT.md glossaries, and ADRs. Use when the user wants Codex to challenge a plan, sharpen terminology, resolve design decisions one-by-one, update domain context docs as decisions crystallize, or record durable architectural decisions without separating the interview from documentation work.
---

# Grill With Docs

Run an interactive design interview that treats documentation as part of the conversation. Challenge the plan against the repository's existing language and decisions, inspect code before asking factual questions, and update docs when the conversation resolves durable domain terms or architectural choices.

## Core Workflow

1. Identify the plan, scope, and current uncertainty.
2. Inspect existing repository docs before asking questions the repo can answer.
3. Build a working decision tree of goals, constraints, domain terms, boundaries, interfaces, persistence, failure handling, migration, testing, and rollout.
4. Resolve the next blocking branch with one question at a time.
5. Recommend a concrete answer with each question, including the trade-off behind it.
6. Update `CONTEXT.md` immediately when a domain term or relationship becomes clear.
7. Offer an ADR only when the decision is durable, surprising, and trade-off driven.

Do not dump a questionnaire. Ask one focused question, wait for the user's answer, update the working model, then continue.

## Repository Discovery

Look for documentation in this order:

- `CONTEXT-MAP.md` at the repository root.
- Root `CONTEXT.md`.
- Context-local `CONTEXT.md` files near the modules affected by the plan.
- Root or context-local `docs/adr/`.
- README, architecture notes, RFCs, issue docs, schemas, tests, and similar features.

If `CONTEXT-MAP.md` exists, treat the repository as multi-context. Use the map to find context-specific glossaries and ADR directories. If there is no map, assume a single root context unless the codebase clearly says otherwise.

Create documentation lazily. Do not create `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/adr/` until the conversation produces content worth recording.

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

Use `references/context-format.md` for structure. Keep `CONTEXT.md` domain-facing:

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

Use `references/adr-format.md` for numbering and format.

Do not create ADRs for obvious choices, easy-to-reverse preferences, or decisions that are better captured as glossary language.
