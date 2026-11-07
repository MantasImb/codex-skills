# codex-skills

## Development workflow

`grill-with-docs` → `to-prd` → `prd-to-plan` → `implement` → manual QA

| Stage | Purpose |
| --- | --- |
| [grill-with-docs](grill-with-docs/SKILL.md) | Start from an issue or description, investigate the repository, and resolve decisions through focused questions. Update reusable domain language/invariants in `CONTEXT.md` and significant architectural rationale in ADRs. |
| [to-prd](to-prd/SKILL.md) | Capture requirements, scope, resolved decisions, assumptions, and deferrals in a PRD, with a matching local issue. Development grilling creates this when concluded unless requested otherwise. |
| [prd-to-plan](prd-to-plan/SKILL.md) | Review independently verifiable phases, dependencies, and verification methods; save the implementation plan in `plans/`. Reference PRD decisions rather than duplicating them. |
| [implement](implement/SKILL.md) | Execute the selected scope using TDD and the appropriate adapter, repository checks, requirements/documentation audit, CodeRabbit review, and a final chat report with manual QA steps. |

### Rules to keep in mind

- **Reuse decisions.** The PRD owns feature decisions; the plan owns execution and evidence. Preserve story/criterion/phase IDs (`US-`, `AC-`, `PH-`). Revisit settled choices only for material new evidence or blockers, updating the affected documents.
- **Start implementation explicitly.** Creating a PRD or plan does not start coding. Invoke `implement` for delivery; same-scope bug, review, and QA follow-ups in that chat retain the workflow without reinvocation. Changes stay reviewable; commits and publication require their own authorization.
- **Choose the pace once.** Default to one phase at a time, pausing for inspection and direction. Request the full plan to run through its dependencies in one go. Reuse the chosen mode on continuation.
- **Verify behavior.** TDD proceeds one behavior at a time: RED → GREEN → refactor. Expected results must be independently justified. Tests must prove the required boundary; passing isolated tests does not establish untested persistence, runtime, or browser behavior. Record actual outcomes and gaps.
- **Audit before repairs.** Compare the task delta against requirements and repository guidance, present findings, then fix clear in-scope problems. Changes to agreed requirements or conflicting guidance need a targeted decision.
- **Review at delivery.** `implement` owns CodeRabbit; standalone TDD does not run it. Review after the full plan, triage findings, fix accepted issues, and revalidate. After material review-driven changes, run one final review. If a genuine attempt fails, disclose the observed failure and incomplete review, then continue under the skip policy; other required checks still apply.
- **Separate implementation from acceptance.** Run agent checks during phases, but deliver one consolidated manual QA checklist after the full plan. Overall status stays `awaiting manual QA` until you confirm it passed. Requirement defects or regressions reopen affected phases; recheck affected QA items after fixes.
- **Defer unrelated work visibly.** Capture actionable out-of-scope findings as small local issues, reusing repository conventions or `issues/`. Link them in the recap/report without expanding scope. Filing an issue does not resolve a current blocker or authorize its fix.

Clearly scoped bugs or small changes can enter `implement` directly without a PRD/plan. A PRD without a plan uses `prd-to-plan` as a fallback, with phase review before execution.

For understanding or documentation sessions, use [grill-me](grill-me/SKILL.md), or `grill-with-docs` when maintaining domain docs/ADRs; finish with the requested output rather than requiring a PRD. Use [prototype](prototype/SKILL.md) when exploration helps resolve a decision, retaining local evidence until review and agreed cleanup. Explicitly invoke [BTW](BTW/SKILL.md) for a read-only side-agent question; inline fallback requires your agreement.

## Business systems

[grill-business](grill-business/SKILL.md) develops and improves business systems through focused discussion and incremental documentation. It separates business context, system-development records, and operational resources; uses outcome-based branch checkpoints; and requires explicit adoption before replacing working instructions. It is independent of the software development workflow above.

## Reference skills from another repository

Use a Git submodule to keep another developer's skills in `references/external-skills/`. The source repository stays separate, and this repo records the exact commit used as a reference.

Add a repository (replace `DEVELOPER/REPO` with its GitHub owner and name):

```bash
git submodule add https://github.com/DEVELOPER/REPO.git references/external-skills
git commit -m "Add external skills reference"
```

Update the reference to the latest upstream version:

```bash
git submodule update --remote references/external-skills
git add references/external-skills
git commit -m "Update external skills reference"
```

When cloning this repo, use `git clone --recurse-submodules <repo-url>`. For an existing clone, run `git submodule update --init --recursive` to download the referenced skills.
