---
name: grill-me
description: Run a requested interactive review of a proposal or repository/documentation goal using focused questions and evidence to resolve decisions and assumptions. Use for stress-testing or guided exploration; ordinary explanation requests do not start an interview. Use grill-with-docs when domain-doc/ADR maintenance is wanted.
---

# Grill Me

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

Run an interactive review until important unknowns are answered, disproven by evidence, or explicitly deferred. Inspect repository facts before asking the user, and ask questions that unlock the next decision rather than an exhaustive questionnaire.

## Establish the Goal

Start from the supplied proposal, issue, document, or typed goal. Read relevant artifacts before asking foundational questions they can answer. Infer the goal and clarify only genuine ambiguity:

- Development: resolve product, architecture, implementation, migration, or rollout decisions.
- Understanding: explain the repository or clarify a concept against its evidence.
- Documentation: develop the requested document, such as a study plan.

Identify the objective, scope, success criteria, and relevant constraints. Ask about users, operators, or rollout only when applicable. Follow explicit goal changes during the conversation. Grilling does not itself start application or test implementation.

`grill-with-docs` is suitable when the session also needs domain glossary or ADR maintenance. Do not require a PRD or route every session through a development pipeline.

## Track Decision Dependencies

Treat the topic as a decision tree. For each meaningful branch, identify its prerequisite, downstream decisions, and current state: resolved, assumed, unknown, conflicted, or explicitly deferred.

Prioritize unknown or conflicted decisions that block progress toward the session goal. Ask from the current set of unblocked decisions; dependent questions wait for their prerequisite answers. Reuse settled decisions unless new evidence materially changes them.

Keep the tree proportional to the goal. Development may require ownership, interfaces, state, persistence, failure handling, permissions, testing, and rollout decisions. An understanding or study-plan session needs its own learning questions, not an imposed implementation checklist.

## Investigate Before Asking

Inspect relevant code, tests, configuration, docs, ADRs, and similar features to resolve factual questions. Distinguish observed facts, inferences, and remaining uncertainty. Ask the user for preferences or policy choices, and for facts only when evidence is absent, ambiguous, or stale.

When evidence contradicts a settled decision, explain the conflict and ask about the affected choice. Do not silently change the intended behavior or reopen the entire interview.

## Ask Focused Questions

One focused question is the default. Include a concrete recommendation and its trade-off for each decision question. Use scenarios to make vague answers precise: an ownership boundary, an acceptable failure outcome, a compatibility constraint, or a measurable success criterion.

You may group two or three short, independent questions when answering one cannot change the meaning or options of another. Handle consequential or larger decisions individually. Do not group dependent questions merely because they concern the same topic.

After each answer, update the model, briefly state what became clear, and move to the next unblocked decision. Avoid questions that are already answered, irrelevant to the goal, or safely deferrable without affecting the current output.

If a branch remains unresolved, identify whether the missing piece is evidence, conceptual clarity, or a user preference. Investigate evidence directly; keep decisions requiring the user's judgment in the main conversation.

## Optional Branch Investigation

Use a narrowly scoped subagent only when delegation is authorized and an independent investigation would help an unresolved branch. Otherwise continue directly. Do not delegate merely because discussion has not immediately settled a question.

Give the agent the raw question and minimum relevant artifacts, with a read-only investigation scope. Avoid supplying the preferred answer or unrelated conversation history. Request evidence, alternatives, and coverage limits, then reconcile useful conclusions into the decision tree.

Use the current runtime's supported lifecycle operations: stop assigning work when the branch is settled or abandoned, interrupt outstanding work if appropriate, and reuse or follow up only while useful. Do not promise a nonexistent close operation. Report actual agent state accurately. Ask the user only about remaining consequential choices, rather than requiring another confirmation of already settled decisions.

## Capture Deferred Local Issues

Capture actionable unrelated bugs or improvements as small local Markdown issues without a separate confirmation for each issue. Reuse repository issue-folder and naming conventions; otherwise use `issues/` and state the location. Check for duplicates and update an existing issue when appropriate.

Record title, problem/opportunity, observed evidence or explicit uncertainty, expected behavior when known, reproduction when available, why it is outside this session's scope, and a brief next step. Link the issues in the closing recap. Creating an issue authorizes neither fixing it nor publishing it externally.

A finding blocking the current goal needs a targeted dependency or scope decision. Filing an issue does not resolve that blocker or expand the session's scope.

## Finish According to the Goal

Conclude when the requested output has enough clarity and evidence, with remaining unknowns explicitly non-blocking and deferred. For development, this means the relevant decisions support the intended next step; for understanding, the requested questions are answered with evidence and limits; for documentation, the requested document is ready at the agreed depth.

If the user asks to pause, stop with current decisions and open work. If they change goals, adapt the interview and final output. Do not claim readiness while blocking questions remain unresolved.

Deliver the requested explanation or document and a concise recap of settled decisions, assumptions, explicit deferrals, remaining blockers, and deferred issue links. Use chat or the existing document being developed; do not require a separate handoff file. Avoid duplicating the recap when the output already records it clearly.

Do not automatically invoke `to-prd`, `prd-to-plan`, or implementation. A user-requested PRD can consume the settled discussion, but concluding `grill-me` alone does not require one.
