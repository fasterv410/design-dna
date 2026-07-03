---
description: Run the full Design DNA method on a reference — capture, measure, distill, tokenize, lab, verify, record. The round-one command that turns a screenshot into REFERENCE.md + tokens.css + a verified rebuild.
argument-hint: [path/to/reference.png | URL | short brief]
---

Run the **complete Design DNA method** on the reference below, using the
`design-dna` skill. This is the full round-one pass — it produces the token
system from scratch.

Reference: $ARGUMENTS

Work through all seven steps in order, producing each artifact before the next:

1. **Capture** — load the reference(s); state the device scale you'll use to
   convert pixels to layout units.
2. **Measure** — pull exact colors, type sizes, spacing, radii, and shadows from
   real pixels. Never guess a value; show the measured numbers.
3. **Distill** — write `REFERENCE.md`: palette with semantic roles, type scale,
   spacing/radius law, depth model, named principles, and a name for the direction.
4. **Tokenize** — emit `tokens.css` with a raw layer and a semantic layer; include
   light and dark sets if the product needs both.
5. **Lab** — rebuild a 1:1 replica in an isolated sandbox using only the tokens.
   Flag any token you had to add to make it match.
6. **Verify** — measure the rebuild against the reference with
   `getBoundingClientRect` and color sampling; report deltas against a 1–3px /
   exact-hex threshold. Iterate until it passes.
7. **Record** — write an ADR for the direction (supersede, don't delete).

Keep the output original work — extract the *system*, don't republish the
reference's assets or branding. If a step is blocked (missing scale, unreadable
region, no sandbox), say so and propose how to unblock it.

### Examples

```
/dna:extract ./references/dashboard.png
/dna:extract https://example.com/pricing
/dna:extract ./ref-light.png and ./ref-dark.png — need both themes
```

> Only need part of the pipeline? Use `/dna:measure` (numbers only),
> `/dna:tokens` (just the token layer), or — once tokens exist — `/dna:build` to
> make new screens without re-measuring.
