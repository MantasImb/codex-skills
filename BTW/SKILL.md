---
name: BTW
description: Use only when the user explicitly invokes the BTW skill for a side-question branch. Reuse an existing read-only BTW sub-agent when available; otherwise create one with the current conversation and repository context, and return only a concise synthesized answer to the main thread.
---

# BTW

Use this skill only when the user explicitly invokes `BTW`.

Do not activate this skill based on conversational language such as "by the way" or similar phrasing. This skill is for intentional branching, not natural-language matching.

## Purpose

This skill handles side questions that should be explored separately from the main conversation while still using:
- the current conversation context
- the current repository and workspace context

The goal is to keep the main thread clean while still answering a context-aware question.

## Required behavior

When this skill is invoked:

1. Reuse the existing BTW sub-agent if one has already been created for this conversation and is still suitable for the new side question.
2. Spawn a new sub-agent only if there is no existing BTW sub-agent to reuse, or if the prior one is no longer usable for the task.
3. When creating a new sub-agent, use `fork_context: true`.
4. Treat the current repository and workspace as part of the investigation context.
5. Keep the BTW sub-agent read-only unless the user explicitly asks for code or file changes.
6. Have the BTW sub-agent investigate only the side question that prompted the invocation.
7. Return only the distilled answer to the main thread.

Do not answer the branched question directly in the main thread before delegating to the BTW sub-agent.

## Activation

Use this skill only when the user explicitly invokes `BTW`.

Do not use this skill:
- because the user says "by the way"
- because the question is merely tangential
- because delegation seems convenient

This skill is reserved for explicit invocation.

## Reuse policy

The default behavior is to keep using the same BTW sub-agent across multiple BTW questions in the same conversation.

Reuse the existing BTW sub-agent when:
- it is still active or can be resumed
- the new question is another side-question in the same overall conversation
- the required behavior is still read-only

Create a fresh BTW sub-agent only when:
- no prior BTW sub-agent exists
- the prior BTW sub-agent is no longer available
- the prior BTW sub-agent has become unsuitable or overly tangled for the new question
- the user explicitly asks for a fresh branch

When reusing an existing BTW sub-agent, send the new side question to that sub-agent instead of creating a new one.

## Scope

Use this skill when the user wants:
- a side-question handled in a separate branch
- current conversation context preserved
- repository-aware reasoning
- the main thread kept free of the exploratory back-and-forth

Do not use this skill for:
- ordinary inline questions
- direct implementation work by default
- file edits, refactors, commits, or migrations unless the user explicitly asks for them

## Sub-agent instructions

The BTW sub-agent should:
- use the inherited conversation context
- inspect the current repository as needed
- remain focused on the current side question
- stay read-only by default
- avoid unrelated exploration
- produce a concise result
- include file references when useful
- state uncertainty clearly when context is insufficient

## Main-thread behavior

The main thread should:
- route BTW side-questions to the reusable BTW sub-agent
- avoid repeating the BTW sub-agent's full exploration log
- present only the concise synthesized result
- preserve focus on the original conversation

## Prompt template

When creating a new BTW sub-agent, use a prompt in this shape:

"You are the reusable BTW sidecar for this conversation. Use the inherited conversation context and the current repository state. Stay read-only unless explicitly told otherwise. Handle side questions sent from the main thread. For each question, return a concise answer with the key conclusion, supporting findings, relevant file references if useful, and any uncertainty."

When reusing an existing BTW sub-agent, send a narrow follow-up in this shape:

"Handle this next BTW side question in the same read-only context: <question>. Return a concise answer with the key conclusion, supporting findings, relevant file references if useful, and any uncertainty."

## Output expectations

Preferred response shape from the BTW sub-agent:
- direct answer
- brief supporting findings
- relevant file references if needed
- explicit assumptions or uncertainty if applicable
