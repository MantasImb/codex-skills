---
name: tdd-rust-backend
description: Test-driven development for Rust backend services using red-green-refactor. Use when building or fixing Rust domain, application, async service, repository, or HTTP backend behavior with cargo test, request/response tests, integration tests, trait-backed ports, or lightweight fakes.
---

# Rust Backend TDD Adapter

This skill adapts the shared TDD workflow for Rust backend services.

## Load First

Use the shared TDD skill as the source of truth:

- Read [../tdd/SKILL.md](../tdd/SKILL.md) for the red-green-refactor workflow, horizontal-slice warning, planning checklist, tracer bullet loop, and cycle checklist.
- Read [../tdd/tests.md](../tdd/tests.md) when choosing test shape or reviewing whether a test verifies behavior.
- Read [../tdd/mocking.md](../tdd/mocking.md) when deciding whether to use a real dependency, test database, in-memory repository, fake, or mock.
- Read [../tdd/interface-design.md](../tdd/interface-design.md) when changing services, ports, repositories, handlers, or crate APIs.
- Read [../tdd/deep-modules.md](../tdd/deep-modules.md) and [../tdd/refactoring.md](../tdd/refactoring.md) before refactoring after GREEN.

Do not duplicate the shared workflow in your reasoning or output. Apply it, then add the Rust-specific decisions below.

## Use This For

- Rust backend domain, application, service, repository, adapter, or HTTP behavior.
- Async services and trait-backed ports.
- Request/response tests for handlers, routers, or apps.
- `cargo test` workflows across crates, packages, or integration tests.

## Public Test Surface

Choose the narrowest public Rust surface that proves the behavior:

- Domain function, value type, aggregate, or crate API.
- Application use case, command/query handler, or service method.
- Trait-backed port when the trait represents a real external boundary.
- Handler, router, or app for HTTP behavior.
- `tests/` integration test when behavior spans modules, adapters, or crates.

Avoid testing private methods, internal call counts, lock usage, concrete repository internals, database rows, or private types when public behavior can prove the outcome. Moving code between modules should not break tests when public behavior is unchanged.

## Rust Boundaries

Keep internal collaborators real. Mock or fake only true system boundaries:

- External APIs, SDKs, databases, queues, network, file system, process boundaries.
- Time and randomness.
- Other services outside the crate or process.

Prefer small hand-written fakes and in-memory repositories over broad mock frameworks. Use a real test database when persistence behavior is the contract. Do not introduce a trait only for testing when there is no meaningful boundary.

Keep ports small and intent-specific. Methods such as `get_order` and `save_order` are easier to fake than generic request methods that push branching into every test fake.

## Red-Green Commands

Use focused `cargo test` commands:

```bash
cargo test checkout_confirms_valid_cart
cargo test -p game_server checkout_confirms_valid_cart
```

After focused GREEN and refactor steps, run the relevant broader Rust suite before closing.

## End Report

Include a concise "Tests implemented" list:

- Behavior or test name.
- Scope: `unit`, `integration`, `api/handler`, or repository-native equivalent.
- File path.
- Focused and broader `cargo test` commands run, including unrelated remaining failures.
