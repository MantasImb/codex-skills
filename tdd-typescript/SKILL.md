---
name: tdd-typescript
description: Apply shared TDD to requested test-first TypeScript library, package, service, or Node behavior using existing runners and public contracts. Use for clear TDD/behavior-test implementation requests or as an implement adapter; framework-neutral work only, not Next.js runtime/DOM behavior.
---

# TypeScript TDD Adapter

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

This skill adapts the shared TDD workflow for framework-neutral TypeScript.

## Load First

Use the shared TDD skill as the source of truth. Resolve its installed location from the available skills; the links below describe this repository layout. If installed separately, resolve the same resources relative to the located `tdd` folder rather than assuming sibling paths.

- Read [../tdd/SKILL.md](../tdd/SKILL.md) for red-green-refactor, settled-decision reuse, independently justified expectations, and test-boundary selection.
- Read [../tdd/tests.md](../tdd/tests.md) when choosing test shape or reviewing whether a test verifies behavior.
- Read [../tdd/mocking.md](../tdd/mocking.md) when deciding whether to mock, fake, or use real collaborators.
- Read [../tdd/interface-design.md](../tdd/interface-design.md) when changing an exported API or dependency boundary.
- Read [../tdd/deep-modules.md](../tdd/deep-modules.md) and [../tdd/refactoring.md](../tdd/refactoring.md) before refactoring after GREEN.

If the shared TDD skill or a required resource cannot be found, report the missing dependency instead of claiming its workflow was applied.

Do not duplicate the shared workflow in your reasoning or output. Apply it, then add the TypeScript-specific decisions below.

## Use This For

- TypeScript libraries and package APIs.
- Node services, application modules, and handlers.
- Exported functions, classes, hooks-free services, or public module contracts.
- Existing Jest, Vitest, Bun test, Node test runner, or repository-specific TypeScript test setups.

Use `tdd-nextjs-jest` instead when React rendering, Next.js App Router behavior, server actions, route handlers in a Next runtime, or Testing Library DOM behavior are part of the public contract.

## Public Test Surface

Reuse an agreed public test boundary. Otherwise choose a public TypeScript boundary that proves the requested behavior; prefer a higher existing boundary when it provides meaningful coverage without unnecessary setup:

- Exported function or value object.
- Public class or service method.
- Package entrypoint.
- Application use case or command/query handler.
- HTTP or message handler when that handler is the module's public boundary.

Avoid testing private helpers, internal module wiring, constructor calls, call order, or file layout. A refactor that preserves exported behavior should not break the test.

Package or service tests prove their public contracts with the collaborators exercised. They do not establish HTTP routing, serialization, real persistence, or an external service's behavior when those boundaries are bypassed or faked. Use real handler/server, persistence, or integration checks when those are part of the requirement, and report any remaining gap.

## TypeScript Boundaries

Keep internal project modules real. Mock or fake only true system boundaries:

- External APIs, SDKs, databases, queues, network, file system, environment, child processes.
- Time and randomness.
- Expensive process boundaries that are not the behavior under test.

Prefer small typed fakes or explicit dependency objects over broad `jest.mock`, `vi.mock`, or module-level mocks. Specific boundary methods such as `getUser` or `createOrder` are easier to fake than generic request methods that require conditionals in test setup.

## Red-Green Commands

Discover the existing runner, package scripts, workspace configuration, and focused filters from the repository. Use that setup instead of selecting a new runner or guessing a command from the language alone. Check current runner documentation when changing configuration or using unfamiliar options.

After focused GREEN and refactor steps, run the relevant broader TypeScript suite before closing.

## End Report

Read [../tdd/reporting.md](../tdd/reporting.md) for the shared chat-report policy. Describe the actual boundary using package/API, application/service, HTTP/message handler, real persistence, or repository-native terminology; distinguish faked boundaries from real integration coverage. Under `implement`, contribute evidence to its consolidated report.
