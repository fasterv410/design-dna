# ADR template — adopting a design direction

Copy this into your project's `docs/adr/` when you adopt a design DNA. Number
it in sequence. **Supersede, don't delete** — if a later direction replaces
this one, mark this one `Superseded by ADR-XXXX` and keep the file.

```markdown
# NNNN. Adopt "<Direction Name>" design DNA

Date: YYYY-MM-DD

## Status

Accepted   <!-- or: Superseded by ADR-XXXX -->

## Context

- Where the reference came from (who shared it, what it is).
- Link to the REFERENCE.md with the measured analysis.
- What the previous direction was, and why it is changing.
- Any rules this new direction breaks from the old one (list them explicitly).

## Decision

1. Adopt "<Direction Name>" as the current design direction.
2. Which token values change (canvas, ink, accent, viz-*), with measured hex.
3. New token layers introduced (data-viz, depth/elevation, motion).
4. Where the language is proven first (the lab pages) before production.

## Consequences

- What renders differently immediately once tokens change.
- What is provisional and still needs work (e.g. "dark mode is a first-pass
  derivation; audit before shipping any dark production surface").
- Scope notes: which surfaces are sanctioned to change, which still wait.

## Alternatives considered

- Other directions you weighed and why you did not pick them.
```

## Why record this

A design direction is a decision with consequences across the whole product. An
ADR makes the *why* durable, so six months later nobody re-litigates a settled
call — and if the direction is replaced, the trail shows what changed and what
it cost.
