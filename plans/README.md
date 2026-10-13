# Skill improvement plans

Status: drafts for later iteration. Created 2026-10-13.

These plans capture the recommendations from the comparison with the local Matt Pocock reference at `49dd158` (2026-10-09). They authorize no skill implementation by themselves.

## Settled direction

- Keep the existing skills independently usable and add `implement` as their coordinator.
- Move CodeRabbit ownership entirely from TDD to `implement`, including standalone TDD usage.
- Preserve one-behavior-at-a-time TDD, refactoring after GREEN, discovery-only grilling, and audit-first reporting.
- Carry approved decisions between stages; ask again when new evidence changes scope, contracts, or risk.
- Prefer Codex-compatible instructions and use repository conventions for artifacts and verification.

Target cycle: `grill-with-docs ↔ prototype when useful → to-prd → prd-to-plan → implement`.

## Plans

| Plan | Purpose | Depends on |
| --- | --- | --- |
| [01: Workflow handoffs](01-workflow-handoffs.md) | Shared decisions, approvals, and requirement traceability | None |
| [02: TDD](02-tdd.md) | Independent expected values, agreed boundaries, remove CodeRabbit | 01; coordinate rollout with 12 |
| [03: TDD adapters](03-tdd-adapters.md) | Apply the shared contract to TypeScript, Next.js/Jest, and Rust | 02 |
| [04: Grill with docs](04-grill-with-docs.md) | Durable discovery handoff | 01 |
| [05: Grill me](05-grill-me.md) | Choose questions by dependencies | 01 |
| [06: Prototype](06-prototype.md) | Shareable logic demos and retained decision evidence | None |
| [07: Branch doc audit](07-branch-doc-audit.md) | Requirements review and complete change scope | 01 |
| [08: BTW](08-btw.md) | Supported delegation with explicit invocation | 11 |
| [09: To PRD](09-to-prd.md) | Test boundaries and reusable approvals | 01 |
| [10: PRD to plan](10-prd-to-plan.md) | Dependencies, progress evidence, migration exception | 01, 09 |
| [11: Codex compatibility](11-codex-compatibility.md) | Portable composition, invocation metadata, clear triggers | None |
| [12: Implement](12-implement.md) | Coordinate implementation, audit, CodeRabbit, and completion | 02, 03, 07, 10, 11, 13 |
| [13: Final QA](13-final-qa.md) | Evidence report and concrete manual checklist | 01 |

## Suggested order

1. Agree the handoff contract and iterate on `implement`, audit, and QA responsibilities.
2. Deliver `implement` and the TDD ownership change together; update adapters and audit.
3. Update PRD and planning handoffs, then refine grilling, prototypes, and BTW.
4. Check compatibility and activation across the finished set.

Parallel integration branches, automatic commits, PR publication, and upstream `implement-spec` orchestration are outside these drafts.
