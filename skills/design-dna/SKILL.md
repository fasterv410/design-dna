---
name: design-dna
description: Reverse-engineer a design system from reference images. Use when someone shares a screenshot, app, or website whose look they want to copy or learn from, and asks you to extract the colors, type, spacing, and feel, turn them into reusable design tokens, and rebuild the UI faithfully. Triggers include "match this design", "extract the colors from this screenshot", "make it look like this app", "build a design system from this reference", or "pixel-match this mockup".
license: MIT
---

# Design DNA

Take a screenshot of a design someone admires and turn it into a real,
reusable design system: colors measured from actual pixels, a semantic token
layer, an isolated lab that proves the tokens, and a decision record that
explains the direction. The goal is a faithful rebuild you can trust — not a
vibe-based guess.

**One rule above all: measure, don't guess.** Eyeballing a hex code is how you
end up 15% off on every color. Sample the pixels.

## When to use this

- Someone shares reference images and wants that look reproduced or learned from.
- You are starting a design system and have a visual target to anchor it.
- You need to prove a rebuild matches the original, not just "looks close".

## When not to use this

- The work is purely functional with no visual target (skip to normal coding).
- You were asked to invent an original look from scratch with no reference.
- The reference is copyrighted and the goal is to republish it as-is — see
  [Ethics & copyright](#ethics--copyright).

## The method

Seven steps. Do them in order. Each one produces an artifact the next one uses.

```
1 Capture  →  2 Measure  →  3 Distill  →  4 Tokenize  →  5 Lab  →  6 Verify  →  7 Record
  images       pixels        REFERENCE.md   tokens.css     replica   numbers      ADR
```

### 1. Capture

Collect the reference images at the highest resolution available. Note the
**device scale** (e.g. an iPhone screenshot is often 3x — 1320px wide file =
440pt of layout). You need the scale to convert measured pixels into layout
units later. Save originals; never edit over them.

### 2. Measure (pixels, not vibes)

Pull real values out of the image. Do not describe colors from memory.

- **Color** — crop a flat region of each surface/text/accent and read its hex.
  On macOS: `sips` to crop, then sample the pixel. See
  [references/measuring-colors.md](references/measuring-colors.md) for exact
  commands. Record the raw hex for every distinct color you can find.
- **Type** — crop a line of text, count its cap-height in pixels, divide by the
  device scale to get the point/rem size. Do the same for each level in the
  hierarchy (display, title, body, caption). Note weight and letter-spacing.
- **Spacing & radius** — measure gaps, padding, and corner radii in pixels,
  convert by the device scale. Look for a rhythm (are gaps multiples of 4? 8?).
- **Depth** — describe every shadow/inset/border you see: color, blur, offset,
  spread. Note whether depth comes from shadows, layering, or hairlines.

Write measured values as exact numbers. Precision here is the whole point.

### 3. Distill the DNA

Turn raw measurements into a written character study: `REFERENCE.md`. Cover:

- **Palette** — each measured color with its **semantic role** (canvas, card,
  sunken, ink, muted-ink, accent, and any data-viz hues), not just a hex list.
- **Typography** — the scale, the pairing strategy, where weight does the work.
- **Spacing & radius law** — the rhythm and the rounding rule.
- **Depth model** — how the design creates layering.
- **Principles** — the 3–6 sentences that explain *why it feels the way it
  does* ("number-first hierarchy", "one loud accent, everything else quiet",
  "borderless cards separated by shadow"). This is the actual DNA.
- **Name the direction** — give it a memorable name. It becomes shared language.

### 4. Tokenize

Convert the DNA into a **semantic token layer** — the single source of truth
the UI reads from. Keep two layers separate:

- **Raw values** — the measured primitives (`--indigo-500: #6b5cff`).
- **Semantic tokens** — roles that map to raw values (`--color-accent: var(--indigo-500)`).

Rules that keep tokens honest:

- Name tokens by **role**, never by appearance (`--color-danger`, not `--color-red`).
- **Data-viz colors are semantic to the data**, not decoration — a color means
  "good/warn/bad" or a specific series, and is only ever used on data ink
  (rings, ticks, sparklines, stat numbers), never on buttons or surfaces.
- Ship **light and dark as parallel token sets** from the start if the product
  needs both. Dark is a real derivation, not `invert()` — lift accents, cut
  chroma, swap shadows for hairlines/elevation.
- Keep values in whatever format the reference demands for fidelity (raw hex is
  fine early); you can convert to `oklch` later without changing what renders.

### 5. Lab — build a throwaway replica

Before touching production, rebuild a **1:1 replica of the reference** in an
isolated sandbox (a `/lab` route group, a Storybook story, a scratch page)
using **only the tokens**. This is a test bed, not a shipping surface. Its job
is to prove the token set is complete and correct.

Isolation rules for the lab (and they **must not leak** into production):

- Hardcoded strings are fine — the goal is pixel fidelity, not i18n.
- Arbitrary one-off values are allowed where needed to match the image.
- If the replica needs a token you didn't define, that's the signal — go back
  to step 4 and add it. The lab surfaces gaps you can't see in a spec.

### 6. Verify by measurement

Do **not** approve the rebuild by looking at it. Screenshots lie; your eye
rounds off. Compare with numbers.

- Render the lab and the reference at the same size.
- Read real geometry from the DOM: `getBoundingClientRect()` on each key
  element, compare against the pixel positions you measured in step 2.
- Sample rendered colors back out and diff them against the target hex.
- Set an acceptance threshold (e.g. **within 1–3px** on position/size, exact on
  color) and record the deltas. Iterate until it passes.
- See [references/verifying-fidelity.md](references/verifying-fidelity.md).

A common trap: a screenshot looks "20px off" but the measured delta is 1px —
trust the number, not the glance. And the reverse: something looks fine but is
measurably wrong. Numbers settle it.

### 7. Record the decision

Write a short **ADR** (Architecture Decision Record) capturing the direction:
what you adopted, what older rules it overrides, what is still provisional
(e.g. "dark mode is a first-pass derivation, needs a real audit before
shipping"). **Supersede, don't delete** — keep the history. See
[references/adr-template.md](references/adr-template.md).

Then promote the proven language from the lab into production — carrying the
tokens and principles, leaving the lab-only shortcuts behind.

## Guardrails

- **Measure, don't guess.** Every color and size comes from a pixel, not memory.
- **Separate raw from semantic.** Tokens name roles; raw values are an
  implementation detail underneath.
- **Lab before production.** Prove the tokens in a sandbox; never debut them on
  a real user surface.
- **Verify with numbers.** `getBoundingClientRect` and color diffs, not vibes.
- **Record decisions.** ADRs, superseded not deleted.
- **Isolation stays isolated.** Lab shortcuts (hardcoded copy, arbitrary
  values) never leak into production.

## Ethics & copyright

Reference images are for **analysis and learning**. Extract the system — the
color relationships, the spacing rhythm, the principles — and rebuild it as
**your own original work**. Do not republish someone else's app screenshots,
copy their exact content/branding, or pass their UI off as yours. A design
*approach* is fair to learn from; a specific brand's assets are not yours to
ship. When in doubt, change the content and make the output your own.

## Definition of done

- [ ] `REFERENCE.md` — measured palette (with roles), type scale, spacing/radius
      law, depth model, named principles.
- [ ] `tokens.css` (or equivalent) — raw + semantic layers, light/dark if needed.
- [ ] A lab replica that renders using only the tokens.
- [ ] A verification pass with recorded deltas that meet the threshold.
- [ ] An ADR recording the direction and what it supersedes.
- [ ] Output is original work, not redistributed reference assets.

## References

- [measuring-colors.md](references/measuring-colors.md) — crop and sample exact
  colors and sizes from an image (macOS + cross-platform notes).
- [verifying-fidelity.md](references/verifying-fidelity.md) — measure the
  rebuild against the reference in the browser.
- [adr-template.md](references/adr-template.md) — the decision record template.
