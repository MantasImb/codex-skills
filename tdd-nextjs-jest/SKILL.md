---
name: tdd-nextjs-jest
description: Apply shared TDD to requested test-first Next.js work using an existing Jest and React Testing Library setup. Use for clear TDD/behavior-test implementation requests involving components, hooks, routes, or actions, or as an implement adapter; not merely because Next.js is mentioned.
---

# Next.js Jest TDD Adapter

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

This skill adapts the shared TDD workflow for Next.js applications tested with Jest and React Testing Library.

## Load First

Use the shared TDD skill as the source of truth. Resolve its installed location from the available skills; the links below describe this repository layout. If installed separately, resolve the same resources relative to the located `tdd` folder rather than assuming sibling paths.

- Read [../tdd/SKILL.md](../tdd/SKILL.md) for red-green-refactor, settled-decision reuse, independently justified expectations, and test-boundary selection.
- Read [../tdd/tests.md](../tdd/tests.md) when checking whether a test verifies behavior rather than implementation.
- Read [../tdd/mocking.md](../tdd/mocking.md) when deciding whether a Next.js module, app dependency, or external service is a mockable boundary.
- Read [../tdd/interface-design.md](../tdd/interface-design.md) when changing component props, route/action contracts, or extracted TypeScript functions.
- Read [../tdd/deep-modules.md](../tdd/deep-modules.md) and [../tdd/refactoring.md](../tdd/refactoring.md) before refactoring after GREEN.

If the shared TDD skill or a required resource cannot be found, report the missing dependency instead of claiming its workflow was applied.

Do not duplicate the shared workflow in your reasoning or output. Apply it, then add the Next.js-specific decisions below.

## Use This For

- Next.js components tested through rendered DOM.
- Pages, layouts, metadata helpers, and App Router route handlers.
- Server actions, hooks, API routes, redirects, cache invalidation, cookies, and headers.
- Jest, `next/jest`, jsdom, React Testing Library, and `userEvent` workflows.

Use `tdd-typescript` instead when the behavior is framework-neutral TypeScript and React or Next.js runtime behavior is not part of the contract.

## Public Test Surface

Reuse an agreed public test boundary. Otherwise choose a public Next.js boundary that proves the requested behavior; prefer a higher existing boundary when it provides meaningful coverage without unnecessary setup:

- Component: render the meaningful public component and assert accessible DOM and interactions.
- Page or layout: assert meaningful output, metadata helpers, redirects, or data-loading behavior through public exports.
- Route handler: call exported `GET`, `POST`, or other handlers with `Request` objects and assert status, headers, and body.
- Server action: call the action as the public boundary and assert returned state, redirect/notFound behavior, cache invalidation, or follow-up public reads.
- Hook: render through a test component or hook helper and assert observable state transitions.
- Extracted utility: use `tdd-typescript` style behavior tests.

Avoid testing private child components, implementation props, internal state, or snapshots as the primary proof. Moving logic between components, hooks, or helpers should not break tests when user-visible behavior is unchanged.

DOM tests prove rendered behavior in the test environment. Direct route/action export tests prove the invoked contract; they do not by themselves prove Next.js routing, framework request context, navigation, server/client integration, or real browser behavior. Mocked redirects or cache calls establish the requested call, not its runtime effect. Add running-app request checks or browser verification when those effects are required, and disclose gaps.

Check the project's Next.js/Jest versions and current testing support before choosing a seam for async Server Components. The [official Next.js Jest guide](https://nextjs.org/docs/app/guides/testing/jest) currently recommends E2E tests for async Server Components because Jest does not support them. Use supported runtime/E2E coverage for the component flow; test extracted logic separately when useful without claiming it proves that flow.

## Next.js Boundaries

Prefer real app components, hooks, and modules you own. Mock framework and system boundaries narrowly:

- `next/navigation` for router, pathname, params, search params, redirects, or `notFound`.
- `next/cache` when cache invalidation is the observable framework call.
- `next/headers` when cookies or headers are part of behavior.
- `next/image` only when the test environment cannot render it usefully.
- Network, SDK, database, time, randomness, file-system, or process boundaries.

Use Testing Library queries that match user perception: `getByRole`, `getByLabelText`, `getByText`, `findBy...`, `waitFor`, and `userEvent`. Keep accessibility intact while making tests pass.

## Red-Green Commands

Discover the repository's Jest scripts, configuration, workspace setup, and focused filters. Use the configured Jest runner, including when another package manager launches it; do not substitute another runner merely because that package manager is available. Check current documentation when changing framework/runner configuration or using unfamiliar options.

After focused GREEN and refactor steps, run the relevant broader Jest suite before closing.

## End Report

Read [../tdd/reporting.md](../tdd/reporting.md) for the shared chat-report policy. Use DOM/component, page, direct route-handler/server-action, hook, running-app request, browser/E2E, or repository-native terminology. Distinguish mocked framework calls from verified runtime effects. Under `implement`, contribute evidence to its consolidated report.
