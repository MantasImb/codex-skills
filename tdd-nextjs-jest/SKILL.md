---
name: tdd-nextjs-jest
description: Test-driven development for Next.js applications tested with Jest and React Testing Library. Use when building or fixing Next.js pages, app router routes, server actions, React components, hooks, API routes, or UI behavior with Jest, jsdom, next/jest, and behavior-focused DOM or request tests.
---

# Next.js Jest TDD Adapter

This skill adapts the shared TDD workflow for Next.js applications tested with Jest and React Testing Library.

## Load First

Use the shared TDD skill as the source of truth:

- Read [../tdd/SKILL.md](../tdd/SKILL.md) for the red-green-refactor workflow, horizontal-slice warning, planning checklist, tracer bullet loop, and cycle checklist.
- Read [../tdd/tests.md](../tdd/tests.md) when checking whether a test verifies behavior rather than implementation.
- Read [../tdd/mocking.md](../tdd/mocking.md) when deciding whether a Next.js module, app dependency, or external service is a mockable boundary.
- Read [../tdd/interface-design.md](../tdd/interface-design.md) when changing component props, route/action contracts, or extracted TypeScript functions.
- Read [../tdd/deep-modules.md](../tdd/deep-modules.md) and [../tdd/refactoring.md](../tdd/refactoring.md) before refactoring after GREEN.

Do not duplicate the shared workflow in your reasoning or output. Apply it, then add the Next.js-specific decisions below.

## Use This For

- Next.js components tested through rendered DOM.
- Pages, layouts, metadata helpers, and App Router route handlers.
- Server actions, hooks, API routes, redirects, cache invalidation, cookies, and headers.
- Jest, `next/jest`, jsdom, React Testing Library, and `userEvent` workflows.

Use `tdd-typescript` instead when the behavior is framework-neutral TypeScript and React or Next.js runtime behavior is not part of the contract.

## Public Test Surface

Choose the public Next.js surface that users, HTTP callers, or framework callers observe:

- Component: render the meaningful public component and assert accessible DOM and interactions.
- Page or layout: assert meaningful output, metadata helpers, redirects, or data-loading behavior through public exports.
- Route handler: call exported `GET`, `POST`, or other handlers with `Request` objects and assert status, headers, and body.
- Server action: call the action as the public boundary and assert returned state, redirect/notFound behavior, cache invalidation, or follow-up public reads.
- Hook: render through a test component or hook helper and assert observable state transitions.
- Extracted utility: use `tdd-typescript` style behavior tests.

Avoid testing private child components, implementation props, internal state, or snapshots as the primary proof. Moving logic between components, hooks, or helpers should not break tests when user-visible behavior is unchanged.

## Next.js Boundaries

Prefer real app components, hooks, and modules you own. Mock framework and system boundaries narrowly:

- `next/navigation` for router, pathname, params, search params, redirects, or `notFound`.
- `next/cache` when cache invalidation is the observable framework call.
- `next/headers` when cookies or headers are part of behavior.
- `next/image` only when the test environment cannot render it usefully.
- Network, SDK, database, time, randomness, file-system, or process boundaries.

Use Testing Library queries that match user perception: `getByRole`, `getByLabelText`, `getByText`, `findBy...`, `waitFor`, and `userEvent`. Keep accessibility intact while making tests pass.

## Red-Green Commands

Use the repository's existing Jest setup and focused filters:

```bash
npm test -- checkout-form
pnpm jest checkout-form
bun test checkout-form
```

After focused GREEN and refactor steps, run the relevant broader Jest suite before closing.

## End Report

Include a concise "Tests implemented" list:

- Behavior or test name.
- Scope: `component`, `page`, `route-handler`, `server-action`, `hook`, `unit`, or repository-native equivalent.
- File path.
- Focused and broader Jest commands run, including unrelated remaining failures.
