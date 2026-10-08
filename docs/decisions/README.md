# Decision records

One short file for each significant decision (stack, hosting, libraries, structure),
so anyone can see later *why* the project is the way it is.

## Naming

`NNNN-short-title.md`, numbered in order: `0001-tech-stack.md`, `0002-hosting.md`, ...
Decision records are never deleted. If a decision changes, write a new record and
mark the old one "Superseded by NNNN".

## Template

```markdown
# NNNN. Title

- **Date:** YYYY-MM-DD
- **Status:** Accepted | Superseded by NNNN

## Decision
What we chose, in one or two sentences.

## Options considered
- Option A: one line
- Option B: one line

## Why this one
The reasons, tied to the project's needs (quality, zero budget, maintainability).

## Trade-offs
What we give up or need to watch out for.
```

## Records

None yet. The first, `0001-tech-stack.md`, is written in Phase 2.
