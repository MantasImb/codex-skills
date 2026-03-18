---
name: grill-me
description: Interrogate product, architecture, implementation, and migration plans until the plan reaches a shared and operationally useful level of clarity. Use when a user wants Codex to stress-test a proposal, walk every branch of the design tree, resolve decision dependencies one-by-one, surface hidden assumptions, or turn a vague plan into a concrete execution model. Especially useful for RFCs, feature plans, refactors, system design notes, rollout plans, and codebase changes where some answers should be discovered by inspecting the repository instead of asking the user.
---

# Grill Me

## Overview

Drive an interactive plan review that keeps digging until the important unknowns are either answered, disproven by repository evidence, or explicitly deferred. Prefer targeted investigation over broad speculation, and prefer one decisive question over a large batch of shallow questions.

## Operating Mode

Treat the plan as a decision tree, not a prose document.

For every branch:
- Identify the parent decision.
- Identify what downstream decisions depend on it.
- Resolve the dependency in the highest-leverage order.
- Ask only the next question that materially unlocks progress.

If the answer may already exist in the codebase, inspect the codebase first. Ask the user only when repository evidence is absent, ambiguous, stale, or policy-driven.

Do not dump a questionnaire. Run an interview.

## Workflow

### 1. Establish the Plan Artifact

Pin down what is being designed before interrogating details.

Extract or ask for:
- Objective
- Scope boundaries
- Intended users or operators
- Success criteria
- Time or rollout constraints
- Existing artifacts to inspect first: code, docs, tickets, RFCs, schemas, tests

If the user provided a document or codebase, read it before asking foundational questions that it can answer.

### 2. Build the Decision Tree

Convert the plan into a compact internal model:
- Goals and non-goals
- Hard constraints
- Major architectural choices
- Data and state model
- Interface boundaries
- Operational concerns
- Validation and rollout strategy

For each item, label it mentally as one of:
- Resolved
- Assumed
- Unknown
- Conflicted
- Deferred

Prioritize `Unknown` and `Conflicted` items that block many other decisions.

### 3. Explore Before Asking

Use the repository to answer factual questions whenever possible.

Inspect:
- Existing modules that would own the change
- Current interfaces, schemas, config, and API boundaries
- Tests that reveal intended behavior
- Docs, ADRs, and comments that encode prior decisions
- Similar features or migrations already implemented

When reporting what you found, distinguish clearly between:
- Facts observed in the codebase
- Inferences from those facts
- Remaining questions for the user

### 4. Interrogate Branches One-by-One

Ask one short, high-value question at a time unless several questions are tightly coupled and cheaper to answer together.

Every question should have a reason. Prefer questions like:
- Which of these two constraints is actually binding?
- Is this state authoritative here or mirrored from another system?
- What failure is acceptable: stale data, blocked writes, or partial rollout?
- Does this need backward compatibility, or can old callers break?
- Is the real requirement configurability, auditability, latency, or simplicity?

Avoid questions that are merely exhaustive but not decision-relevant.

After each answer:
- Update the decision tree
- State what became clear
- State what remains open
- Move to the next blocking dependency

### 5. Force Precision

When the user answers vaguely, tighten the abstraction instead of accepting fuzzy language.

Convert vague statements into concrete choices:
- "Fast" -> latency or throughput target
- "Simple" -> fewer moving parts, less code, less operator burden, or less user friction
- "Support retries" -> idempotent writes, deduplication, or resumable workflow
- "Scalable" -> which dimension grows and what bottleneck matters

When multiple interpretations remain plausible, present the alternatives and ask the user to choose.

### 6. Check the Missing Surfaces

Before concluding, explicitly close or defer the major surfaces below:
- Inputs and outputs
- Ownership and source of truth
- Persistence and migrations
- Concurrency and failure handling
- Permissions and security boundaries
- Observability and debugging
- Performance and capacity assumptions
- Backward compatibility
- Test strategy
- Rollout, fallback, and recovery

Do not require every plan to be equally detailed. Match depth to risk.

## Questioning Heuristics

Prefer questions that:
- Eliminate multiple downstream ambiguities
- Expose hidden constraints
- Separate policy decisions from implementation details
- Reveal incompatibilities with the existing codebase
- Convert preferences into measurable requirements

Deprioritize questions that:
- Are already answerable from local artifacts
- Do not affect design or execution
- Can wait until a later implementation phase without creating rework

## Response Shape

Keep the conversation moving. A good turn usually contains:
- A one- or two-sentence summary of the current model
- Any codebase findings that changed the picture
- The single next question, or a tightly related pair

When useful, show a short checkpoint list of:
- Resolved decisions
- Open decisions
- Explicit assumptions

## Stop Condition

Stop the interview only when one of these is true:
- The plan is concrete enough to implement safely
- The remaining unknowns are explicitly deferred and non-blocking
- The user asks to pause or switch modes

Before stopping, summarize:
- Final shared understanding
- Decisions made
- Assumptions still in force
- Risks or unanswered questions that remain

## Example Triggers

Use this skill for prompts like:
- "Interrogate this architecture plan until there are no hidden assumptions left."
- "Walk this refactor proposal branch-by-branch and tell me what you need to know."
- "Review this migration plan, explore the repo for answers first, and only then question me."
- "Turn this vague feature idea into an implementation-ready plan by interviewing me."
