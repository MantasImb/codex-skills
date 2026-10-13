# Logic Prototype

Use an interactive demo to explore business rules, state transitions, or data shape. If the question is primarily visual design, use [UI.md](UI.md).

## State the Question and Choose the Runtime

Write the question, assumptions, and format choice in the artifact. Reuse the shared evidence, handoff, and adoption policy in [SKILL.md](SKILL.md).

Default to a self-contained HTML file for exploring a model with stakeholders. It should open directly in a browser, without installation, a server, build tooling, remote scripts, or remote assets. Use plain HTML, CSS, and JavaScript to make the state and actions visible. Explain when a browser model simplifies or omits native behavior.

Use a terminal app in the project's existing runtime when that runtime or native behavior is essential: actual domain types, process behavior, concurrency, or a persistence mechanism being evaluated. Do not port a native question to browser JavaScript and imply equivalent verification. Reuse existing tooling rather than adding a new runtime just for exploration.

## Keep the Model Inspectable

Put the model behind a small interface appropriate to the question: a reducer, explicit state machine, pure functions, or a state-owning module. Keep display/input handling separate enough that the rules can be inspected. Avoid abstractions that do not help answer the question.

The model is prototype code too. A portable interface makes the evidence easier to inspect; it does not exempt later production adoption from normal tests and error handling.

## HTML Demo

Show these in one understandable view:

- The question and any important assumptions or simplifications.
- Current relevant state, including derived values or invariants being explored.
- Clearly named actions and inputs for the scenarios under discussion.
- A reset control restoring the initial fixture and clearing exploration history.
- Enough action/result history to explain surprising transitions, when useful.

Keep state in memory. Show rejected actions and their reasons when legality is part of the question; do not silently swallow invalid transitions. Include representative fixtures or scenario presets when they reduce setup effort. Prioritize readable state and actions over visual polish.

## Terminal Demo

Render current state and available actions in a stable view. Read a key or line, dispatch the action, and refresh state after each change. Include reset and quit, with simple discoverable controls. Use the project's existing terminal conventions; avoid new UI dependencies unless they materially help the native question.

Provide one clear launch command using the existing runtime/task runner. Add a task-runner entry only when useful and consistent with repository conventions; otherwise document the direct command.

## Verify and Hand Over

Exercise the key transitions, rejected actions when relevant, and reset. Verify the actual open/launch path. Report what was observed and what was simplified or untested; agent exploration alone does not establish user acceptance.

Give the user the artifact link or launch command and a few useful actions/scenarios to try. Incorporate feedback as the model evolves. Follow [SKILL.md](SKILL.md) for recording a provisional or evaluated verdict, retaining evidence, and agreed cleanup.
