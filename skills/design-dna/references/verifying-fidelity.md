# Verifying fidelity by measurement

Approve a rebuild with numbers, not with your eyes. This file shows how to
compare the lab replica against the reference measurements you took in step 2.

## Read real geometry from the DOM

Render the lab page, then measure the actual elements the browser laid out.
Run this in the DevTools console (or any browser-automation eval):

```js
// Report position + size of the elements you care about.
const targets = ['#dial', '#big-number', '.card', '.cta']
console.table(
  targets.map((sel) => {
    const el = document.querySelector(sel)
    if (!el) return { sel, found: false }
    const r = el.getBoundingClientRect()
    return {
      sel,
      x: Math.round(r.x),
      y: Math.round(r.y),
      w: Math.round(r.width),
      h: Math.round(r.height),
    }
  })
)
```

Compare each number against the pixel position/size you measured from the
reference (converted to the same unit). The delta is your fidelity score.

## Sample rendered colors back out

Confirm a token actually renders the target hex:

```js
const el = document.querySelector('.card')
getComputedStyle(el).backgroundColor   // "rgb(255, 255, 255)"
// convert to hex and diff against the measured target
```

For a full-surface check, screenshot the rendered page and sample the same
crop offsets you used on the reference — the two hex values should match.

## Acceptance thresholds

| Dimension            | Threshold                          |
|----------------------|------------------------------------|
| Element position     | within 1–3px of target             |
| Element size         | within 1–3px of target             |
| Surface / text color | exact match on hex                 |
| Accent color         | exact match on hex                 |
| Type size            | within 0.5pt / 1px                 |

Record the deltas in a small table and iterate until every row passes. If a
value can't pass, decide explicitly: is the reference measurement wrong, or is
a token wrong? Fix the cause, not the symptom.

## Two traps to remember

- **The eye rounds off.** A layout can *look* 20px low while the measured delta
  is 1px. Trust the number.
- **A screenshot can look right and be wrong.** Something that "looks fine" may
  be measurably off. The number is the source of truth either way.

## Optional: pixel diff

For a whole-screen check, overlay the rendered capture on the reference at the
same resolution and diff them (any image-diff tool, or a canvas
`globalCompositeOperation = 'difference'`). Bright pixels are where they
disagree — a fast way to spot a missed radius, gap, or weight.

## Responsive & theme checks

If the product ships multiple breakpoints or themes, verify each one — the
tokens should hold at 320 / 375 / 768 / 1024 / 1440 and in both light and dark.
Measure, don't assume the small screen "probably works".
