# Design DNA

Reverse-engineer a design system from a reference image, then rebuild it
faithfully. This file is the portable, tool-agnostic version of the method —
Codex, Gemini CLI, Cursor, and any agent that reads `AGENTS.md` will pick it
up. (In Claude Code the same method ships as the `design-dna` skill.)

You can also **copy this file into your own project's root** so your coding
agent follows the method there.

## When it applies

Someone shares a screenshot, app, or website whose look they want reproduced or
learned from, or you're anchoring a new design system to a visual target.

## The one rule

**Measure, don't guess.** Sample real pixels. Never type a hex code or a size
from memory — that is how every value ends up subtly wrong.

## The method — seven steps, in order

Each step produces an artifact the next step uses.

1. **Capture** — collect the reference images at full resolution. Note the
   device scale (a 3x phone screenshot: a 1320px-wide file = 440pt of layout).
   You need the scale to convert measured pixels into layout units.

2. **Measure** — pull exact values from pixels:
   - Colors: crop a flat region and read the hex with an eyedropper.
   - Type: cap-height in px ÷ device scale = point/rem size. Note weights.
   - Spacing & radius: measure in px, convert by scale, look for a rhythm (4? 8?).
   - Depth: describe every shadow/inset/border (color, blur, offset, spread).
   Record exact numbers.

3. **Distill** — write `REFERENCE.md`: the palette with **semantic roles**
   (canvas, card, sunken, ink, muted-ink, accent, data-viz hues), the type
   scale, the spacing/radius law, the depth model, 3–6 **named principles**
   that explain why it feels the way it does, and a **name** for the direction.

4. **Tokenize** — emit design tokens in two layers: **raw** primitives
   (`--indigo-500: #6b5cff`) and **semantic** roles that map to them
   (`--color-accent: var(--indigo-500)`). Name tokens by role, never by
   appearance. Data-viz colors are semantic to the data and used only on data
   ink (rings, ticks, sparklines, stat numbers) — never on buttons or surfaces.
   Ship light and dark as parallel sets if the product needs both; dark is a
   real derivation, not `invert()`.

5. **Lab** — rebuild a **1:1 replica** of the reference in an isolated sandbox
   (a scratch route, a Storybook story) using **only the tokens**. This proves
   the token set is complete. If the replica needs a token you didn't define,
   that's the gap — add it. Lab shortcuts (hardcoded copy, arbitrary values)
   must not leak into production.

6. **Verify** — measure the rebuild against the reference. Read geometry with
   `getBoundingClientRect()` and sample rendered colors; compare to the values
   from step 2. Threshold: within **1–3px** on geometry, **exact** on color.
   Record the deltas and iterate. Trust the number over your eye — a layout can
   look 20px off while the real delta is 1px.

7. **Record** — write an ADR for the direction (supersede, don't delete), then
   promote the proven language from the lab into production, leaving the
   lab-only shortcuts behind.

## Ethics & copyright

Reference images are for **analysis**. Extract the system — the color
relationships, the spacing rhythm, the principles — and rebuild it as **your
own original work**. Do not republish someone else's app screenshots, copy
their branding, or pass their UI off as yours.

## Definition of done

- `REFERENCE.md` with measured palette (roles), type scale, spacing/radius law,
  depth model, named principles.
- A token file with raw + semantic layers (light/dark if needed).
- A lab replica rendered only from tokens.
- A verification pass with recorded deltas that meet the threshold.
- An ADR recording the direction.
- Output is original work, not redistributed reference assets.
