---
description: Measure exact colors, type sizes, spacing, and radii from a reference image — the raw numbers only, no tokens and no build. Use when you just want to know what's actually in a screenshot.
argument-hint: [path/to/reference.png | URL]
---

Do **steps 1–2 of the Design DNA method only** — Capture and Measure. Pull real
values out of the reference and report them. Do not tokenize, do not build.

Reference: $ARGUMENTS

Follow the "measure, don't guess" rule from the `design-dna` skill and its
[measuring-colors reference](../skills/design-dna/references/measuring-colors.md):

1. **Capture** — note the source resolution and the **device scale** (e.g. a 3x
   phone screenshot: 1320px file = 440pt layout). You need it to convert pixels.
2. **Measure** — crop flat regions and sample real pixels:
   - **Color** — the exact hex of every distinct surface, text, and accent color.
   - **Type** — cap-height in pixels ÷ device scale → point/rem size, per level
     (display, title, body, caption); note weight and letter-spacing.
   - **Spacing & radius** — gaps, padding, and corner radii in pixels, converted;
     call out the rhythm (multiples of 4? 8?).
   - **Depth** — every shadow/inset/border: color, blur, offset, spread.

Output a **measured-values table** with exact numbers and where each came from.
Flag anything you couldn't read cleanly rather than guessing it.

### Examples

```
/dna:measure ./references/card.png
/dna:measure ./hero-3x.png    (state the 3x scale in the output)
```

> Next step: feed these numbers into `/dna:tokens` to build the semantic token
> layer, or run the whole thing at once with `/dna:extract`.
