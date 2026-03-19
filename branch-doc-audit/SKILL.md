---
name: branch-doc-audit
description: Audit the current branch, unpushed commits, or working-tree diff against repository documentation and engineering guidance, then report misalignments before proposing or making changes. Use when a feature has been implemented and Codex should verify alignment with architecture docs, clean-code guidance, testing expectations, feature documentation, ADRs, READMEs, or other repository-defined standards before updating code or docs.
---

# Branch Doc Audit

## Overview

Compare the code delta to the repository's documented expectations and produce an explicit drift report before changing anything. Treat this as an audit-first workflow: establish what changed, establish what the docs claim, then enumerate mismatches and missing documentation before deciding on fixes.

## Workflow

### 1. Define the Audit Surface

Identify what to compare before reading broadly.

Determine the change set from the user's request or local git state:
- Current working-tree diff
- Unpushed commits on the current branch
- Full branch diff against a base branch
- A specific PR or commit range if the user supplied one

State explicitly which source of truth you are using for the delta.

### 2. Gather Only the Relevant Documentation

Start from files touched by the diff and fan out only to documentation that governs those areas.

Inspect, in roughly this order:
- Local docs nearest to the changed code: module READMEs, architecture notes, ADRs, design docs
- Repository-wide engineering guidance: clean architecture notes, testing guides, coding standards
- Existing tests that reveal intended behavior
- User-facing docs that describe features, behavior, configuration, or APIs

Prefer repository evidence over assumptions. If guidance appears duplicated or contradictory, note the conflict instead of forcing a conclusion.

### 3. Spawn Audit Agents Deliberately

Default to one subagent for small or medium changes.

Use one audit subagent when:
- The diff is modest and concentrated in one subsystem
- The same docs cover both implementation and quality expectations
- The cost of duplicate repo reading would outweigh any parallelism

Use two subagents when the audit naturally splits into distinct questions:
- Agent A: code and feature drift
  Compare behavior, interfaces, configuration, and feature claims against docs and tests.
- Agent B: standards drift
  Compare the change against architecture guidance, clean-code conventions, layering rules, and testing expectations.

Choose two agents only when their scopes are disjoint enough that each can own a clear question and produce a separate report. Avoid spawning multiple agents that all reread the same files and repeat the same findings.

If you spawn agents:
- Give each agent a tightly-scoped prompt
- Tell each agent to report findings only, not make changes
- Ask for file references and concrete evidence
- Integrate the reports into a single deduplicated mismatch summary

### 4. Produce the Drift Report Before Any Changes

Before suggesting edits, present a report with these sections:
- Scope audited
- Docs and guidance consulted
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
4. Re-run the audit summary mentally and confirm the mismatch list is closed

Prefer fixing the source of truth first. If docs are clearly stale and code is otherwise sound, recommend doc updates instead of code churn.

## Prompt Pattern

Use prompts shaped like:
- `Use $branch-doc-audit to compare my current branch against the repository docs and list all misalignments before making changes.`
- `Use $branch-doc-audit to audit the unpushed diff for architecture, testing, and documentation drift.`
- `Use $branch-doc-audit to review this feature branch against the repo's ADRs and READMEs, then tell me whether code or docs should change.`

## Output Rules

Keep the final audit concise and evidence-based.

Always:
- Lead with findings, not process narration
- Reference the files that define the expectation
- Separate facts from inferences
- Call out what was not checked if the audit surface was incomplete

Never:
- Make code or docs edits before presenting the mismatch list, unless the user explicitly overrides that order
- Treat absence of documentation as proof that the implementation is correct
- Inflate weak hunches into findings without concrete repository evidence
