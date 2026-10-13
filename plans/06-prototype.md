# Plan: Prototype formats and retained evidence

Status: draft. Targets: `prototype/SKILL.md`, `prototype/LOGIC.md`, `prototype/UI.md`, metadata.

## Outcome

Choose a prototype format that answers the question and retain the evidence behind the validated decision.

## Changes

- Add a self-contained HTML logic demo for stakeholder feedback, with visible question, state, actions, and reset; require no installation.
- Keep terminal logic prototypes when the project's runtime or native behavior is central to the question. Explain the format choice.
- Preserve structurally different UI variants in their real app context, with stubbed mutations and production exclusion.
- Capture the verdict, question, limitations, and artifact/branch pointer in the handoff or issue before cleanup.
- Keep prototype code out of the production result; validated logic still needs normal production tests and error handling when adopted.
- Use existing artifact conventions; preserving evidence does not itself authorize commits or publication.

## Acceptance criteria

- [ ] A stakeholder can open the HTML demo and explore/reset the model.
- [ ] A native-runtime question can still use the terminal format.
- [ ] The decision record links to inspectable evidence after production cleanup.
- [ ] Winning prototype code is validated under production expectations when adopted.

## Open decision

- Default evidence location: local artifact, existing issue attachment, or a throwaway branch when commits are authorized?
