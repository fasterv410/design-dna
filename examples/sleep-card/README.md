# Worked example — a "Sleep Quality" card

This folder shows the artifacts the Design DNA method produces, run on a small
**invented** reference (a sleep-quality summary card). Everything here is
original — there are no third-party screenshots. It's here so you can see what
"done" looks like before you run the method on your own reference.

## The (invented) reference

Picture a single card from a wellness app:

- An off-white page with one white card floating on it.
- A big score — **82** — inside a soft ring that's ~82% filled.
- The label "Sleep score" under it.
- Two rows: "Deep" and "REM", each with a thin colored bar and a value.
- Everything is generously rounded; separation comes from a soft shadow, not
  borders. One indigo accent; the data bars use a calm mint and amber.

## What each step produced

| Step         | Artifact                                                    |
|--------------|-------------------------------------------------------------|
| 2 Measure    | the numbers quoted in `REFERENCE.md`                        |
| 3 Distill    | [`REFERENCE.md`](REFERENCE.md) — palette, type, principles  |
| 4 Tokenize   | [`tokens.css`](tokens.css) — raw + semantic layers          |
| 7 Record     | [`ADR-0001-adopt-soft-instrument.md`](ADR-0001-adopt-soft-instrument.md) |

Steps 5 (Lab) and 6 (Verify) happen in your app, not here — you'd drop a
scratch route in your own project, rebuild the card from `tokens.css`, and
measure it against the reference with `getBoundingClientRect`. The
[verifying-fidelity reference](../../skills/design-dna/references/verifying-fidelity.md)
shows the exact console snippet.

## Try it yourself

In Claude Code (with the plugin installed):

```
/design-dna:create ./path-to-your-reference.png
```

Or just point your agent at a screenshot and say "run the Design DNA method on
this". The output should look like the files in this folder.
