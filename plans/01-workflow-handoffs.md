# Plan: Workflow handoffs

Status: draft. Scope: the shared contract between discovery, PRD, planning, implementation, and audit.

## Outcome

Each stage can continue from recorded decisions without asking the user to repeat settled decisions or losing the requirements behind the work.

## Changes

- Start `grill-with-docs` from an existing issue or a description supplied in the chat. Resolve the decisions needed for the feature, issue, or application, then create the PRD from that concluded discussion using `to-prd`.
- Use the PRD as the source of truth for those decisions: requirements, resolved decisions, explicit assumptions, deferred questions, and agreed scope. Link the source issue when one exists; scale the PRD to the work.
- Keep reusable domain vocabulary and invariants in `CONTEXT.md`, and architectural rationale in ADRs when applicable. The PRD references those documents and records their implications for the proposed work.
- Derive the implementation plan from the PRD. The plan owns phase order, dependencies, execution status, and verification evidence; reference PRD decisions rather than maintaining a second decision record.
- Record agreed public test boundaries with their coverage and limitations.
- Give user stories and acceptance criteria stable identifiers; carry those into phases, verification evidence, and audit findings.
- Use settled decisions from the conversation and PRD. Ask again only when new evidence requires a material change or an unresolved decision blocks progress. Do not add approval metadata or a separate sign-off mechanism.
- Creating the PRD and plan does not start implementation. Starting `implement` is an implementation request for its stated scope. Manual QA checks the delivered behavior separately.
- Have `implement` read the source PRD, its linked domain/architecture guidance, and the implementation plan. Keep decisions made during implementation current in the PRD, with corresponding execution changes in the plan and domain/ADR updates where applicable.
- Use existing PRD and plan templates for the handoff; do not require a separate per-feature handoff document.

## Settled decisions

- Flow: `grill-with-docs` (conversation and domain docs) → `to-prd` (durable feature/application decisions) → `prd-to-plan` (execution plan) → `implement`.
- The PRD owns feature/application decisions; the plan translates them into executable phases.
- The same flow supports an existing issue, a new feature, or a whole application.
- When grilling concludes, create the PRD from the discussion; do not repeat the discovery interview during PRD creation.
- No separate approval tracking is needed. Preserve settled decisions and clearly mark assumptions and unresolved questions.

## Acceptance criteria

- [ ] A settled design can reach TDD without repeated questions about unchanged interfaces or test boundaries.
- [ ] A changed contract produces a targeted decision request and an updated artifact.
- [ ] Each acceptance criterion has a verification method or an explicit remaining gap.
- [ ] A fresh implementation session can recover the agreed decisions from the PRD and linked docs, and its execution scope from the plan.
- [ ] A decision changed during implementation is reflected in the PRD and affected plan sections.

## Implementation detail to resolve in later plans

- Define how `grill-with-docs` hands the concluded discussion to `to-prd` in plans 04 and 09, preserving the agreed flow without another discovery or decision checkpoint.
