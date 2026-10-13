# Plan: Codex compatibility and skill activation

Status: draft. Scope: the requested skills and the proposed `implement` skill.

## Outcome

Skill composition and activation match Codex's available interfaces without importing Claude-specific tool assumptions.

## Changes

- Compose skills by reading and following their authoritative `SKILL.md` files; resolve installed locations instead of assuming a Claude `Skill` tool or sibling layout always exists.
- Use available agent APIs and lifecycle operations. Document inheritance intent and distinguish runtime-specific examples from universal requirements.
- Add or update `agents/openai.yaml` where useful. Use `policy.allow_implicit_invocation: false` for skills deliberately restricted to explicit invocation.
- Keep descriptions concise, with distinct triggers and boundaries; move specialized guidance into conditional references and preserve one source of truth per policy.
- Define commit/publication behavior for `implement`; proposed default is to leave reviewable workspace changes unless separately authorized.
- Validate current Codex documentation during implementation rather than assuming upstream Claude frontmatter controls Codex invocation.

## Acceptance criteria

- [ ] Composite skills can locate/load dependencies without a Claude-specific tool call.
- [ ] Explicit-only skills have matching instructions and invocation metadata.
- [ ] Example prompts select the intended skill and avoid overlapping triggers.
- [ ] Missing dependencies or unsupported tools produce a concrete limitation report.

## Open decision

- Which skills beyond BTW should require explicit invocation, particularly `implement`, discovery, and planning?

Reference: [official skill documentation](https://learn.chatgpt.com/docs/build-skills), checked during the comparison on 2026-10-13.
