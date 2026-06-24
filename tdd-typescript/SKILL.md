---
name: tdd-typescript
description: Test-driven development for TypeScript libraries, application modules, services, and Node code using red-green-refactor. Use when building or fixing TypeScript behavior through exported APIs, public module contracts, existing test runners, boundary mocks, and behavior-focused tests outside framework-specific Next.js Jest workflows.
---

# TypeScript TDD Adapter

This skill adapts the shared TDD workflow for framework-neutral TypeScript.

## Load First

Use the shared TDD skill as the source of truth:

- Read [../tdd/SKILL.md](../tdd/SKILL.md) for the red-green-refactor workflow, horizontal-slice warning, planning checklist, tracer bullet loop, and cycle checklist.
- Read [../tdd/tests.md](../tdd/tests.md) when choosing test shape or reviewing whether a test verifies behavior.
- Read [../tdd/mocking.md](../tdd/mocking.md) when deciding whether to mock, fake, or use real collaborators.
- Read [../tdd/interface-design.md](../tdd/interface-design.md) when changing an exported API or dependency boundary.
- Read [../tdd/deep-modules.md](../tdd/deep-modules.md) and [../tdd/refactoring.md](../tdd/refactoring.md) before refactoring after GREEN.

Do not duplicate the shared workflow in your reasoning or output. Apply it, then add the TypeScript-specific decisions below.

## Use This For

- TypeScript libraries and package APIs.
- Node services, application modules, and handlers.
- Exported functions, classes, hooks-free services, or public module contracts.
- Existing Jest, Vitest, Bun test, Node test runner, or repository-specific TypeScript test setups.

Use `tdd-nextjs-jest` instead when React rendering, Next.js App Router behavior, server actions, route handlers in a Next runtime, or Testing Library DOM behavior are part of the public contract.

## Public Test Surface

Choose the narrowest public TypeScript surface that proves the behavior:

- Exported function or value object.
- Public class or service method.
- Package entrypoint.
- Application use case or command/query handler.
- HTTP or message handler when that handler is the module's public boundary.

Avoid testing private helpers, internal module wiring, constructor calls, call order, or file layout. A refactor that preserves exported behavior should not break the test.

## TypeScript Boundaries

Keep internal project modules real. Mock or fake only true system boundaries:

- External APIs, SDKs, databases, queues, network, file system, environment, child processes.
- Time and randomness.
- Expensive process boundaries that are not the behavior under test.

Prefer small typed fakes or explicit dependency objects over broad `jest.mock`, `vi.mock`, or module-level mocks. Specific boundary methods such as `getUser` or `createOrder` are easier to fake than generic request methods that require conditionals in test setup.

## Red-Green Commands

Use the repository's existing runner and focused filters:

```bash
npm test -- checkout
pnpm test checkout
bun test checkout
vitest checkout
```

After focused GREEN and refactor steps, run the relevant broader TypeScript suite before closing.

## End Report

Include a concise "Tests implemented" list:

- Behavior or test name.
- Scope: `unit`, `integration`, `api/handler`, or repository-native equivalent.
- File path.
- Focused and broader test commands run, including unrelated remaining failures.
