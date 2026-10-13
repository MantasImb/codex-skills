---
name: tdd-rust-backend
description: Apply shared TDD to requested test-first Rust backend behavior through public domain, service, handler, or integration boundaries. Use for clear TDD/behavior-test implementation requests or as an implement adapter; not merely because Rust is mentioned.
---

# Rust Backend TDD Adapter

Select this skill implicitly only for a clear, specific request to perform its workflow. Keywords, topic overlap, explanation-only questions, or speculation about future work do not start it. Follow explicit invocation or intentional composition by an already active workflow within its scope.

This skill adapts the shared TDD workflow for Rust backend services.

## Load First

Use the shared TDD skill as the source of truth. Resolve its installed location from the available skills; the links below describe this repository layout. If installed separately, resolve the same resources relative to the located `tdd` folder rather than assuming sibling paths.

- Read [../tdd/SKILL.md](../tdd/SKILL.md) for red-green-refactor, settled-decision reuse, independently justified expectations, and test-boundary selection.
- Read [../tdd/tests.md](../tdd/tests.md) when choosing test shape or reviewing whether a test verifies behavior.
- Read [../tdd/mocking.md](../tdd/mocking.md) when deciding whether to use a real dependency, test database, in-memory repository, fake, or mock.
- Read [../tdd/interface-design.md](../tdd/interface-design.md) when changing services, ports, repositories, handlers, or crate APIs.
- Read [../tdd/deep-modules.md](../tdd/deep-modules.md) and [../tdd/refactoring.md](../tdd/refactoring.md) before refactoring after GREEN.

If the shared TDD skill or a required resource cannot be found, report the missing dependency instead of claiming its workflow was applied.

Do not duplicate the shared workflow in your reasoning or output. Apply it, then add the Rust-specific decisions below.

## Use This For

- Rust backend domain, application, service, repository, adapter, or HTTP behavior.
- Async services and trait-backed ports.
- Request/response tests for handlers, routers, or apps.
- `cargo test` workflows across crates, packages, or integration tests.

## Public Test Surface

Reuse an agreed public test boundary. Otherwise choose a public Rust boundary that proves the requested behavior; prefer a higher existing boundary when it provides meaningful coverage without unnecessary setup:

- Domain function, value type, aggregate, or crate API.
- Application use case, command/query handler, or service method.
- Trait-backed port when the trait represents a real external boundary.
- Handler, router, or app for HTTP behavior.
- `tests/` integration test when behavior spans modules, adapters, or crates.

Avoid testing private methods, internal call counts, lock usage, concrete repository internals, database rows, or private types when public behavior can prove the outcome. Moving code between modules should not break tests when public behavior is unchanged.

Domain/service tests prove behavior through the exercised collaborators. Trait fakes and in-memory repositories do not prove real adapters or persistence. Use handler/router request tests, real persistence checks, or cross-crate integration tests when the requirement crosses those boundaries. A test in `tests/` is not automatically proof of real infrastructure coverage; report what actually ran and what remains unverified.

## Rust Boundaries

Keep internal collaborators real. Mock or fake only true system boundaries:

- External APIs, SDKs, databases, queues, network, file system, process boundaries.
- Time and randomness.
- Other services outside the crate or process.

Prefer small hand-written fakes and in-memory repositories over broad mock frameworks. Use a real test database when persistence behavior is the contract. Do not introduce a trait only for testing when there is no meaningful boundary.

Keep ports small and intent-specific. Methods such as `get_order` and `save_order` are easier to fake than generic request methods that push branching into every test fake.

## Red-Green Commands

Discover the repository's workspace, package selection, features, test targets, and existing scripts before choosing focused or broader test commands. Reuse its test setup; check current tool documentation when using unfamiliar options or changing configuration.

After focused GREEN and refactor steps, run the relevant broader Rust suite before closing.

## End Report

Read [../tdd/reporting.md](../tdd/reporting.md) for the shared chat-report policy. Use domain/crate API, application/service, handler/router, real persistence, cross-crate integration, or repository-native terminology. Distinguish fakes from real adapter coverage. Under `implement`, contribute evidence to its consolidated report.
