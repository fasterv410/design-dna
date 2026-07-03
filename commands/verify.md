---
description: Measure an existing rebuild against its reference and report the deltas — getBoundingClientRect geometry plus color sampling, within a 1–3px / exact-hex threshold. Settle "does it match?" with numbers, not a glance.
argument-hint: [rebuild: /lab route, URL, or file] vs [reference image]
---

Do **step 6 of the Design DNA method** — Verify by measurement. Compare a rendered
rebuild against its reference and report whether it passes, with real numbers.

Compare: $ARGUMENTS

**Do not approve by looking.** Screenshots lie and the eye rounds off. Per the
`design-dna` skill and its
[verifying-fidelity reference](../skills/design-dna/references/verifying-fidelity.md):

1. Render the rebuild and the reference at the **same size**.
2. Read real geometry from the DOM — `getBoundingClientRect()` on each key element
   — and compare against the pixel positions measured from the reference.
3. Sample the rendered colors back out and diff them against the target hex.
4. Set the threshold (**within 1–3px** on position/size, **exact** on color),
   record every delta in a table, and mark each **pass/fail**.
5. If anything fails, name the specific fix (this padding is 6px, target is 8px)
   and iterate — don't hand-wave "close enough".

Remember the trap in both directions: something that *looks* 20px off may measure
1px, and something that *looks* fine may be measurably wrong. Trust the number.

### Examples

```
/dna:verify http://localhost:3000/lab vs ./references/dashboard.png
/dna:verify ./src/app/lab/page.tsx against ./references/card.png
```

> Building the rebuild in the first place? Use `/dna:build`. Running the whole
> pipeline including this step? `/dna:extract`.
