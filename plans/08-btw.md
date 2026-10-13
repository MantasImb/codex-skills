# Plan: BTW delegation compatibility

Status: draft. Targets: `BTW/SKILL.md`, `BTW/agents/openai.yaml`.
Depends on: [11: Codex compatibility](11-codex-compatibility.md).

## Outcome

An explicitly invoked BTW question uses a reusable, read-only side agent through the available runtime.

## Changes

- Replace the fixed `fork_context: true` instruction with inherited-context intent and supported tool parameters; this desktop session exposes `fork_turns: "all"`.
- Reuse an existing suitable agent, using the runtime's supported follow-up operation to resume an idle agent when needed.
- Keep explicit-only metadata, narrow side-question scope, repository context, and concise synthesis.
- Define behavior when delegation is unavailable: explain the limitation and obtain agreement before changing the requested branching behavior.
- Keep file mutations outside the default side-question scope.

## Acceptance criteria

- [ ] Ordinary “by the way” language does not activate BTW.
- [ ] Two explicit BTW questions can reuse the same suitable agent.
- [ ] The agent receives conversation/repository context and remains read-only.
- [ ] No unsupported tool argument or agent-lifecycle promise remains.

## Open decision

- Should an unavailable side-agent surface use an opt-in inline fallback or simply report the limitation?
