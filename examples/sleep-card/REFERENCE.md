# REFERENCE — "Soft Instrument" (sleep-quality card)

Measured analysis of the reference. All colors sampled from pixels; all sizes
converted from a 3x capture (file px ÷ 3 = pt).

## Palette (measured hex → role)

| Hex       | Role        | Where it's used                        |
|-----------|-------------|----------------------------------------|
| `#F6F6FA` | canvas      | page background                        |
| `#FFFFFF` | card        | the raised card surface                |
| `#EFEFF3` | sunken      | ring track, empty bar track            |
| `#1B1C1E` | ink         | the big score, row values              |
| `#9A9AA2` | muted-ink   | labels, units                          |
| `#6B5CFF` | accent      | the ring's filled arc                  |
| `#2FB79A` | viz-good    | "Deep" bar — data ink only             |
| `#E7B549` | viz-warn    | "REM" bar — data ink only              |

One loud voice: indigo is the only chromatic UI color. The mint and amber are
**data ink** — they carry meaning in the bars and appear nowhere else.

## Typography

Single family, weight does the hierarchy.

| Level    | Size / weight | Notes                          |
|----------|---------------|--------------------------------|
| score    | 46 / 700      | tabular figures, tight tracking|
| title    | 20 / 600      | card and row titles            |
| body     | 15 / 400      | supporting text                |
| caption  | 13 / 500      | labels, units, muted-ink       |

## Spacing & radius law

- Rhythm is a **4-based scale**: 4 · 8 · 16 · 24 · 32.
- Card radius **24**; pills and bars are fully rounded (radius = half height).
- No radius smaller than 12 anywhere — nothing is sharp.

## Depth model

- Cards are **borderless**; separation comes from a single soft shadow
  (`0 6px 20px rgba(24,24,43,0.06)`), not outlines.
- The ring track and bar tracks are **sunken** (a slightly darker fill), giving
  a subtle inset feel without heavy neumorphic shadows.

## Principles (the DNA)

1. **Number-first.** The score is the hero; everything else supports it.
2. **One loud voice.** A single indigo accent; all other color is data ink.
3. **Borderless, shadow-separated.** Surfaces float; no outlines.
4. **Everything rounded.** A generous radius law, nothing sharp.
5. **Quiet by default.** Muted labels, calm data hues, lots of breathing room.

**Direction name: "Soft Instrument."** Precise data, softly presented.
