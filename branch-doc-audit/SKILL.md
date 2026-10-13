---
name: branch-doc-audit
description: Audit a branch or working-tree change against PRD/plan requirements and repository documentation before fixes. Use when the user requests requirements, architecture, testing, or documentation alignment review, or when implement intentionally composes this audit.
---

# Branch Doc Audit

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

## Overview

Compare the task delta to intended requirements and documented expectations. Report requirements coverage separately from standards/documentation drift before fixes. Standalone audit is read-only unless fixes are authorized. Under `implement`, present findings, then let the coordinator repair clear in-scope issues without another approval checkpoint; changes to settled requirements or unresolved guidance conflicts need a targeted user decision.

## Workflow

### 1. Define the Audit Surface

Identify what to compare before reading broadly.

Determine the change set from the user's request or local git state:
- Current working-tree diff
- Unpushed commits on the current branch
- Full branch diff against a base branch
- A specific PR or commit range if the user supplied one

Prefer the explicit scope and baseline supplied by the user or recorded by `implement`. Otherwise inspect Git state to establish a baseline, clarifying genuine ambiguity. State the baseline revision and audited scope, including relevant commits, staged/unstaged changes, and new files. Distinguish pre-existing work from task changes, including in shared files; do not silently attribute the entire dirty workspace to this task.

Load the source PRD, plan, acceptance criteria, and agreed test boundaries when available. Use existing requirement IDs in findings. Missing requirements or documentation are coverage gaps, not evidence of compliance.

### 2. Gather Only the Relevant Documentation

Start from files touched by the diff and fan out only to documentation that governs those areas.

Inspect, in roughly this order:
- Local docs nearest to the changed code: module READMEs, architecture notes, ADRs, design docs
- Repository-wide engineering guidance: clean architecture notes, testing guides, coding standards
- Existing tests that reveal intended behavior
- User-facing docs that describe features, behavior, configuration, or APIs

Prefer repository evidence over assumptions. If guidance appears duplicated or contradictory, note the conflict instead of forcing a conclusion.

### 3. Check Requirements and Standards

For each in-scope requirement, compare implementation and observed verification evidence. Report missing or partial behavior, incorrect behavior, scope creep, and unverified criteria. Distinguish demonstrated coverage from inference; an isolated passing test does not prove untested runtime behavior.

Check documentation and standards separately using the classifications below. Keep audit findings proportional to the task and grounded in concrete evidence.

Use supported subagent APIs only when delegation is authorized and independent scopes justify it. Give agents read-only scopes and require file references and evidence; deduplicate their findings while retaining separate requirements and standards conclusions. Otherwise perform the audit directly.

### 4. Produce the Drift Report Before Any Changes

Before suggesting edits, present a report with these sections:
- Scope audited
- Docs and guidance consulted
- Requirements coverage and verification gaps
- Confirmed alignments
- Misalignments
- Missing documentation
- Conflicts or ambiguities in the documentation
- Recommended next action

For each misalignment, include:
- What changed in code
- What the relevant documentation or tests say
- Why they disagree
- Whether the likely fix is code, docs, tests, or a deliberate policy decision

Do not quietly repair issues during the audit phase. The first deliverable is the mismatch inventory.

### 5. Distinguish Kinds of Misalignment

Classify each finding so the follow-up work is obvious:
- `Behavior drift`: code behavior no longer matches documented behavior
- `Documentation drift`: implementation looks intentional, but docs are outdated or incomplete
- `Architecture drift`: layering, ownership, or dependency direction conflicts with guidance
- `Quality drift`: tests, validation, or observability expectations are missing or inconsistent
- `Ambiguous guidance`: repository docs disagree or are too vague to judge compliance confidently

When uncertain, say so explicitly and name the missing evidence.

### 6. Decide the Fix Order

After the drift report, recommend an order:
1. Clarify ambiguous or conflicting guidance
2. Fix code that violates settled standards or intended behavior
3. Update docs and tests to match the intended state
4. Reinspect affected code/docs and verification evidence after fixes; identify closed and remaining findings

Prefer fixing the source of truth first. If docs are clearly stale and code is otherwise sound, recommend doc updates instead of code churn.

## Prompt Pattern

Use prompts shaped like:
- `Use $branch-doc-audit to compare my current branch against the repository docs and list all misalignments before making changes.`
- `Use $branch-doc-audit to audit the unpushed diff for architecture, testing, and documentation drift.`
- `Use $branch-doc-audit to review this feature branch against the repo's ADRs and READMEs, then tell me whether code or docs should change.`

## Output Rules

Keep the final audit concise and evidence-based.

Deliver results in chat. Under `implement`, feed conclusions into its consolidated report; no separate audit-report file is required.

Always:
- Lead with findings, not process narration
- Reference the files that define the expectation
- Separate facts from inferences
- Call out what was not checked if the audit surface was incomplete

Never:
- Make code or docs edits before presenting the mismatch list, unless the user explicitly overrides that order
- Treat absence of documentation as proof that the implementation is correct
- Inflate weak hunches into findings without concrete repository evidence
