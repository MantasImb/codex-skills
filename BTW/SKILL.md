---
name: BTW
description: Handle a side question in a reusable, read-only agent with conversation and repository context. Use only when the user explicitly invokes the BTW skill; ordinary by-the-way wording or a tangential question does not activate it.
---

# BTW

Use only for an explicit BTW skill request. Preserve the main conversation's focus by delegating the side question and returning a concise synthesis. Do not answer the question inline before delegation.

## Route the Question

1. Identify the side question and its read-only scope. Clarify only if the question itself is ambiguous.
2. Check for a suitable existing BTW agent in this conversation. Reuse it unless unavailable, unsuitable, overly tangled, or the user requests a fresh branch.
3. If none is suitable, create an agent with inherited conversation context and the current repository/workspace context. Use the actual runtime's supported parameters, not an assumed `fork_context` argument.
4. Give the agent only the current side-question task, read-only constraints, and relevant updates since its last investigation. Inheritance provides context, not permission to act on unrelated requests from the main conversation.
5. Obtain its result and synthesize the answer in the main chat, with evidence and uncertainty when useful. Do not replay its exploration log or change the main task's scope.

Explicit invocation requests the side-agent investigation. It does not authorize unrelated agents or external messaging.

## Supported Lifecycle

Describe context inheritance as intent and use the currently available tools. In a Codex runtime exposing the collaboration tools used here:

- New agent: `spawn_agent` with `fork_turns: "all"` inherits the conversation. Include the current repository path and the specific read-only question in its task.
- Running suitable agent: use `send_message` to supply the next question or a correction. It delivers a message but does not start a turn on an idle agent.
- Idle suitable agent: use `followup_task` to resume work on the next question.
- Use supported status/wait operations to obtain results. Retain the agent identity for later explicit BTW questions; do not promise a nonexistent close operation.

These are runtime-specific examples, not universal API names. Check the exposed tool schema before supplying parameters. With another runtime, use its supported equivalents. Agent reuse is limited to this conversation and does not assume agents survive into another chat.

## Scope and Agent Task

Default to read-only investigation: inspect relevant files and other authorized sources, but do not edit files, create issues, refactor, commit, run migrations, publish, or send messages externally. File changes require an explicit request covering those changes; inherited context alone is insufficient.

Give the agent a task shaped like:

> Investigate this BTW side question: <question>. Use inherited conversation context and the current repository at <path>, including these relevant updates: <updates if any>. Stay read-only and focused on this question. Return the direct answer, brief supporting evidence, useful file references, and explicit uncertainty or verification limits. Do not continue or implement the main task.

Do not start multiple investigations on the same busy agent that obscure which question its answer addresses. Finish or explicitly redirect the current question before reusing it for another one.

## Unavailable Delegation

If agent tools are unavailable, no suitable agent can run, or delegation fails, explain the concrete limitation and offer an inline answer. Wait for the user's agreement before investigating or answering in the main chat. Do not silently substitute inline work or claim an agent ran.

Reuse explicit inline-fallback agreement already given for the same question; do not repeat the request. If agreement is absent, leave the side question pending and continue independent main-task work when useful.

## Return the Answer

Lead with the answer, followed by only the supporting findings needed to understand it. Include relevant file/source references and material assumptions or uncertainty. Distinguish agent findings from any added main-chat inference. Preserve the original task and record the agent identity for suitable reuse on later explicitly invoked BTW questions.
