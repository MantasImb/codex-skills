---
name: prototype
description: Build a disposable interactive prototype to answer a design question before production implementation. Use for exploring logic/state models through a self-contained HTML demo or native terminal app, or comparing structurally different UI variants in app context.
---

# Prototype

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

Build the smallest interactive artifact that answers the user's question. Prototype findings inform decisions; they do not automatically authorize production implementation.

## Choose the Format

Infer the question from the request and repository evidence; clarify only if the ambiguity affects what to build. State the question and why the chosen format fits.

- Logic, state transitions, or data shape: read [LOGIC.md](LOGIC.md). Default to a self-contained HTML demo that opens without installation. Use a terminal app when the actual project runtime or native behavior is central to the question.
- Layout, information hierarchy, or interaction design: read [UI.md](UI.md). Compare structurally different variants in the real app context, using one route and a visible switcher.

Respect an explicit format preference. If an assumption is needed, name it in the artifact and handoff rather than silently treating it as a requirement.

## Shared Constraints

- Mark artifacts as prototypes. Reuse local repository artifact conventions and keep the question and run/open instructions discoverable. App-hosted variants follow the existing routing conventions.
- Keep state in memory by default. Stub mutations. When persistence or native integration is itself the question, use clearly identified scratch resources and explain the boundary being exercised.
- Show relevant state after actions and provide a reset to the initial fixture. Keep setup and dependencies minimal: HTML opens directly; terminal/app prototypes use an existing runtime or task runner with a clear launch command.
- Optimize for learning, not production completeness. Add only the validation and handling needed to make exploration useful. Demonstrate the key scenarios and reset before handoff; do not claim a prototype satisfies production testing requirements.
- Keep prototype routes, variants, controls, and mutations out of the production result. A hidden switcher alone is insufficient if a production URL can still select prototype variants.
- Keep scope tied to the question; avoid speculative abstractions or unrelated changes.

## Evidence and Handoff

Default to local artifacts. Hand over an absolute artifact link or run/open instructions, the question, scenarios to explore, observed findings, and limitations. Findings remain provisional until the user evaluates the prototype; if feedback is pending, state that rather than inventing a verdict.

Record the question, user-evaluated verdict (or pending status), limitations, and inspectable artifact pointer in the PRD or existing document appropriate to the session goal. Do not require a PRD for understanding/documentation work, or create a separate notes file when an appropriate record already exists. If no record exists, keep a concise local note with the artifact. Significant architectural conclusions may belong in an ADR under repository conventions.

Retain inspectable evidence until the user has reviewed it and agreed on cleanup. Before deleting runnable artifacts, preserve enough local evidence to explain the evaluated decision: representative screenshots/fixtures, state/action traces, or a compact model excerpt as appropriate. Update decision-record pointers to the retained evidence so they do not link to deleted artifacts. A prose verdict alone may not capture the behavior or alternatives that informed the choice.

Issue attachments, committed throwaway branches, publication, and commits require explicit authorization; evidence retention does not authorize those actions.

## Adoption and Cleanup

A selected variant or validated model is input to production work, not automatic permission to implement it. If adoption is requested, apply normal production tests, error handling, integration verification, and repository standards. Useful logic can be adapted after that validation; the throwaway shell and exploration controls do not become production features.

Separate removal from production paths from deletion of retained evidence. After user-reviewed findings and agreed cleanup, remove exploration scaffolding from the app while preserving the agreed evidence locally and keeping its references valid.
