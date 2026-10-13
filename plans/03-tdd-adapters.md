# Plan: TDD adapter alignment

Status: draft. Targets: `tdd-typescript`, `tdd-nextjs-jest`, `tdd-rust-backend`.
Depends on: [02: TDD](02-tdd.md).

## Outcome

All adapters consume the same approved test-boundary contract and explain the limits of their verification.

## Changes

- Keep the shared TDD skill authoritative; reference its oracle and approval rules instead of duplicating them.
- Replace “narrowest public surface” selection with a boundary that proves the requested behavior. Prefer a higher existing boundary when it provides meaningful coverage.
- TypeScript: distinguish package/service tests from real HTTP, persistence, or external integration verification when those affect the contract.
- Next.js/Jest: distinguish DOM or direct-export tests from runtime/browser verification; mocked framework behavior alone does not prove the complete user flow.
- Rust: distinguish domain/service tests from handler, persistence, and cross-crate integration coverage when relevant.
- Discover runner commands from the repository. Check current framework documentation when changing framework-specific guidance.
- Report behavior, test boundary, file, commands/outcomes, and uncovered requirements. Keep CodeRabbit ownership in `implement`.

## Acceptance criteria

- [ ] Each adapter reuses an approved boundary and uses independently justified expected values.
- [ ] A passing isolated test does not imply untested runtime or integration behavior passed.
- [ ] Existing runner conventions and adapter routing remain clear.

## Open decision

- Use a shared report reference or retain a short adapter-specific report format?
