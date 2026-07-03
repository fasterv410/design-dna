---
description: Turn a reference (or already-measured values) into REFERENCE.md + tokens.css — the semantic design-token layer, raw + semantic, light and dark. Distill and tokenize, no lab build.
argument-hint: [reference.png | Claude Design project | path to measured notes]
---

Do **steps 3–4 of the Design DNA method** — Distill and Tokenize. Turn raw
measurements into the written DNA and a token file. If the input is an image and
no measurements exist yet, measure it first (steps 1–2); if measured values are
already provided, start from them. If the input is a **Claude Design**
(`claude.ai/design`) project, pull it with the `DesignSync` tool — its CSS
variables often *are* the token layer already (see the skill's
[claude-design reference](../skills/design-dna/references/claude-design.md)).

Input: $ARGUMENTS

Per the `design-dna` skill:

**3. Distill → `REFERENCE.md`:**
- **Palette** — each color with its **semantic role** (canvas, card, sunken, ink,
  muted-ink, accent, data-viz hues), not just a hex list.
- **Typography** — the scale, the pairing strategy, where weight does the work.
- **Spacing & radius law** — the rhythm and the rounding rule.
- **Depth model** — how the design creates layering.
- **Principles** — 3–6 sentences on *why it feels the way it does*. This is the DNA.
- **Name the direction** — a memorable name that becomes shared language.

**4. Tokenize → `tokens.css`:**
- Two separate layers: **raw values** (`--indigo-500: #6b5cff`) and **semantic
  tokens** that map to them (`--color-accent: var(--indigo-500)`).
- Name tokens by **role**, never by appearance (`--color-danger`, not `--color-red`).
- **Data-viz colors are semantic to the data** — good/warn/bad or a series — and
  only ever touch data ink, never buttons or surfaces.
- Ship **light and dark as parallel sets** if the product needs both; dark is a
  real derivation (lift accents, cut chroma, swap shadows for hairlines), not `invert()`.

### Examples

```
/design-dna:tokenize ./references/dashboard.png
/design-dna:tokenize ./notes/measured-values.md
```

> Next: prove the tokens with `/design-dna:build` (rebuild the reference in a lab), or
> run everything end-to-end with `/design-dna:create`.
