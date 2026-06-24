# ADR Format

ADRs live in `docs/adr/` and use sequential numbering: `0001-slug.md`, `0002-slug.md`, and so on.

Create `docs/adr/` lazily, only when the first ADR is needed.

## Template

```md
# {Short title of the decision}

{1-3 sentences: what context matters, what was decided, and why.}
```

An ADR may be a single paragraph. The value is recording that a decision was made and why, not filling out a template.

## Optional Sections

Only include optional sections when they add real value.

- `Status` frontmatter: `proposed`, `accepted`, `deprecated`, or `superseded by ADR-NNNN`.
- `Considered Options`: include only when rejected alternatives are worth remembering.
- `Consequences`: include only when non-obvious downstream effects need to be called out.

## Numbering

Scan `docs/adr/` for the highest existing number and increment by one. Use a short lowercase slug:

```text
0007-use-domain-events-for-billing.md
```

## ADR-Worthy Decisions

Create or propose an ADR for:

- Architectural shape.
- Integration patterns between contexts.
- Technology choices with meaningful lock-in.
- Boundary and ownership decisions.
- Deliberate deviations from the obvious path.
- Constraints not visible in the code.
- Rejected alternatives when the rejection is non-obvious.

Skip the ADR when the decision is easy to reverse, unsurprising, or not the result of a real trade-off.
