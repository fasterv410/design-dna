# 0001. Adopt "Soft Instrument" design DNA

Date: 2026-07-04

## Status

Accepted

## Context

We had no shared design language for the wellness dashboard — colors and
spacing were being chosen ad hoc per screen. A reference card (a sleep-quality
summary) was chosen as the visual target. Its measured analysis is in
[REFERENCE.md](REFERENCE.md): a number-first, borderless, softly-rounded look
with one indigo accent and calm data-viz hues.

## Decision

1. Adopt **"Soft Instrument"** as the design direction for the dashboard.
2. Establish the token layer in [tokens.css](tokens.css): raw primitives plus
   semantic roles (`--color-canvas #F6F6FA`, `--color-ink #1B1C1E`,
   `--color-accent #6B5CFF`, and data-viz `--viz-good` / `--viz-warn`).
3. Data-viz colors (mint, amber) are **semantic to the data** and used only on
   data ink — never on buttons or surfaces.
4. Depth is **borderless + soft shadow**; the radius law forbids anything
   sharper than 12px.
5. Prove the language on a lab replica of the reference card before applying it
   to real screens.

## Consequences

- Existing screens re-render on the new canvas and ink the moment tokens land;
  the change is at token level and doesn't touch markup.
- **Dark mode is provisional** — a first-pass derivation (lifted accent, cut
  chroma, hairline instead of shadow). It needs a real audit before any dark
  surface ships.
- Any future "louder" call-to-action must introduce a new accent token rather
  than reusing a data-viz hue.

## Alternatives considered

- **Per-screen styling** (status quo): rejected — it was the reason nothing felt
  coherent.
- **A heavy neumorphic treatment** (deep inset/outset shadows): rejected — it
  reads as skeuomorphic and fails in dark mode; we kept only a subtle sunken
  fill for tracks.
