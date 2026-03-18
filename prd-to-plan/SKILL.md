---
name: prd-to-plan
description: Turn a PRD into a multi-phase implementation plan using tracer-bullet vertical slices, saved as a local Markdown file in ./plans/. Use when the user wants to break down a PRD, create an implementation plan, plan phases from a PRD, or mentions "tracer bullets".
---

# PRD to Plan

Turn an approved PRD into a phased implementation plan built from thin vertical slices. The output is a local Markdown file in `./plans/`.

Work in this order unless the task is already partially complete:
1. Confirm the PRD is present in the conversation or identify the local PRD file.
2. Explore the codebase to ground the plan in the current architecture.
3. Extract the durable decisions that every phase will rely on.
4. Propose tracer-bullet phases as end-to-end vertical slices.
5. Review the phase breakdown with the user and iterate until approved.
6. Write the final Markdown plan into `./plans/`.

## Operating Rules

- Treat each phase as a vertical slice through the full system, not a horizontal layer milestone.
- Prefer many thin slices over a few thick ones.
- Each slice must be demoable, testable, or otherwise verifiable on its own.
- Do not anchor the plan to volatile implementation details such as specific file names, helper names, or internal refactors.
- Do capture durable decisions such as routes, schema shapes, key models, auth boundaries, and third-party integration boundaries.
- Distinguish clearly between repo facts, PRD requirements, and your inferences.
- Do not write the final plan file until the user approves the phase breakdown.

## Workflow

### 1. Confirm the PRD Is in Context

The PRD should already be in the conversation or available as a local file.

If it is missing, ask the user to paste it or point to the file before proceeding.

### 2. Explore the Codebase

Inspect the repository before proposing phases.

Look for:
- Existing product and architecture boundaries
- Current route and API shapes
- Relevant data models and persistence patterns
- Auth and permission mechanisms
- Third-party service touchpoints
- Similar flows or adjacent features

Summarize what the repo clearly shows, what it implies, and what remains uncertain.

### 3. Identify Durable Architectural Decisions

Before slicing the work, extract the decisions that are unlikely to change across phases.

Common categories:
- Routes or URL patterns
- Schema shape and major entities
- Key data models and state transitions
- Authentication and authorization approach
- Third-party service boundaries

These decisions belong near the top of the plan so each phase can build on them.

### 4. Draft Tracer-Bullet Phases

Break the PRD into thin, end-to-end phases.

Each phase should:
- Deliver a narrow but complete path through schema, backend, frontend, and tests when those layers exist
- Cover a coherent subset of the PRD's user stories
- Produce something the team can demo, validate, or learn from

Avoid horizontal slices such as:
- "build the database layer"
- "add all APIs"
- "implement the UI"

Prefer vertical slices such as:
- "first user can create and view a draft item through the main happy path"
- "admin can review and approve one item with basic audit visibility"

### 5. Review the Breakdown with the User

Present the proposed breakdown as a numbered list.

For each phase, show:
- **Title**: short descriptive name
- **User stories covered**: the user stories or PRD sections the phase addresses

Then ask:
- Does the granularity feel right: too coarse or too fine?
- Should any phases be merged or split?

Iterate until the user explicitly approves the breakdown.

### 6. Write the Plan File

Create `./plans/` if it does not already exist.

Write a Markdown file named after the feature, for example `./plans/user-onboarding.md`.

Use this template:

```markdown
# Plan: <Feature Name>

> Source PRD: <brief identifier or link>

## Architectural decisions

Durable decisions that apply across all phases:

- **Routes**: ...
- **Schema**: ...
- **Key models**: ...
- **Auth**: ...
- **External services**: ...

---

## Phase 1: <Title>

**User stories**: <list from PRD>

### What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation.

### Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

---

## Phase 2: <Title>

**User stories**: <list from PRD>

### What to build

...

### Acceptance criteria

- [ ] ...
```

Add, remove, or rename architectural sections when appropriate, but keep the structure focused on durable decisions and thin phases.

## Good Outcome

The skill is complete when:
- The PRD has been translated into clear, tracer-bullet phases
- The phase boundaries match the repo's real architecture
- Durable decisions are explicit and easy to reference
- The user has approved the granularity
- The final Markdown plan has been written to `./plans/`
