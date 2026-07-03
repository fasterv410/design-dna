---
description: Extract a design system from a reference image and rebuild it faithfully — measure, tokenize, lab, verify, record.
argument-hint: [path/to/reference.png or a URL or a short brief]
---

Run the **Design DNA** method on the reference below.

Reference: $ARGUMENTS

Follow the seven steps from the `design-dna` skill, in order, and produce each
artifact before moving on:

1. **Capture** — load the reference(s). State the device scale you'll use to
   convert pixels to layout units.
2. **Measure** — pull exact colors, type sizes, spacing, radii, and shadows
   from real pixels. Never guess a value. Show the measured numbers.
3. **Distill** — write `REFERENCE.md`: palette with semantic roles, type scale,
   spacing/radius law, depth model, the named principles, and a name for the
   direction.
4. **Tokenize** — emit a `tokens.css` with a raw layer and a semantic layer;
   include light and dark sets if the product needs both.
5. **Lab** — rebuild a 1:1 replica in an isolated sandbox using only the
   tokens. Flag any token you had to add to make it match.
6. **Verify** — measure the rebuild against the reference with
   `getBoundingClientRect` and color sampling; report the deltas against a
   1–3px / exact-hex threshold. Iterate until it passes.
7. **Record** — write an ADR for the direction (supersede, don't delete).

Keep the output original work — extract the *system*, don't republish the
reference's assets or branding. If anything blocks a step (missing scale,
unreadable region, no sandbox), say so and propose how to unblock it.
