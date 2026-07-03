# Contributing

Thanks for helping improve Design DNA. It's small on purpose — a method, not a
framework — so contributions should keep it sharp rather than bigger.

## Where things live

- **The method** is `skills/design-dna/SKILL.md`. This is the source of truth.
- **The references** in `skills/design-dna/references/` hold the concrete recipes
  (measuring colors, verifying fidelity, the ADR template).
- **The adapters** (`AGENTS.md`, `adapters/cursor/`, `adapters/windsurf/`,
  `adapters/copilot/`) are condensed mirrors of the method for other tools.

## The one rule for changes

**If you change the method, update every adapter to match.** The seven steps and
the "measure, don't guess" rule must read the same everywhere:

- `skills/design-dna/SKILL.md` (full)
- `AGENTS.md` (portable full)
- `adapters/cursor/design-dna.mdc`
- `adapters/windsurf/design-dna.md`
- `adapters/copilot/copilot-instructions.md`

Adapters can be shorter, but they must not contradict the skill.

## Good contributions

- A clearer or more accurate measurement recipe (especially non-macOS).
- Another tool adapter (with install instructions in the README).
- A better worked example.
- Fixes to the images (sources are the `.svg` files in `assets/`; regenerate the
  `.png` from them).

## Please avoid

- Turning this into a code library or CLI — it's a method for an agent to follow.
- Adding third-party app screenshots. Keep examples original (see the ethics note
  in the README).

## Regenerating the images

The PNGs in `assets/` are rendered from the `.svg` sources. Any tool that
rasterizes SVG works; a headless browser screenshot at 2x is what produced the
current set.
