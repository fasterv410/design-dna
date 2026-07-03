---
description: Write an Architecture Decision Record for a design direction — what you adopted, what it supersedes, what's still provisional. Supersede, don't delete.
argument-hint: [direction name or short description]
---

Do **step 7 of the Design DNA method** — Record the decision. Capture the chosen
design direction as a short ADR so the reasoning survives past the pull request.

Direction: $ARGUMENTS

Use the template at
[adr-template.md](../skills/design-dna/references/adr-template.md) and the rules
from the `design-dna` skill:

- **Context** — what prompted this direction (the reference, the goal, the problem
  with what came before).
- **Decision** — the direction you adopted: the named principles, the palette and
  token strategy, the depth and type approach. Point at `REFERENCE.md` / `tokens.css`
  rather than restating every value.
- **Supersedes** — which older direction or ADR this replaces. **Supersede, don't
  delete** — mark the old one superseded and keep the history.
- **Status & provisional bits** — what's proven vs. still first-pass (e.g. "dark
  mode is a derivation, needs a real audit before shipping").
- **Consequences** — what this locks in and what it rules out.

Number it in sequence with any existing ADRs (`ADR-0002-...`, not a duplicate),
and place it wherever the project keeps decision records (`docs/adr/` is typical).

### Examples

```
/design-dna:adr Soft Instrument — supersedes the Electric Lime direction
/design-dna:adr adopt the measured dashboard palette as our design system
```

> Haven't chosen the direction yet? It comes out of `/design-dna:tokens` (the named
> direction in `REFERENCE.md`) or a full `/design-dna:extract` run.
