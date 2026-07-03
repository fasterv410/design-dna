---
description: Build UI from an EXISTING token set — reuse tokens.css, skip measurement, jump straight to the lab/verify/record steps. The round-two "just the UI" command for new screens on an established design system.
argument-hint: [what to build] from [path/to/tokens.css]
---

Do **steps 5–7 of the Design DNA method** — Lab, Verify, Record — on an
**existing** token system. The DNA is already extracted; this is a build pass,
not an extraction pass.

Request: $ARGUMENTS

**Do not re-measure and do not re-derive tokens.** Read the token file that
already exists and build only from it. If no token path is given, find the
project's `tokens.css` / `REFERENCE.md` and confirm which one you're using.

1. **Read the tokens** — load the existing `tokens.css` (and `REFERENCE.md` if
   present) and use it as the single source of truth. Every color, size, and
   radius comes from a token.
2. **Lab** — build the requested screen/component in the sandbox using **only**
   those tokens. If you find yourself needing a value with no token, stop: that's
   a gap — add the token to the set (a `/design-dna:tokenize`-style change) and note it,
   don't hardcode a one-off into what will ship.
3. **Verify** — if there's a visual target for this screen, measure against it
   (`getBoundingClientRect` + color sampling, 1–3px / exact-hex). If it's a net-new
   screen with no reference, sanity-check that spacing, type, and color all resolve
   to real tokens and match the established rhythm.
4. **Record** — only if this introduces or changes a direction. Reusing the
   existing system needs no new ADR; a new pattern worth keeping does.

The point of this command: on round two you're spending tokens, not measuring
pixels. Keep the extracted DNA fixed and let it pay off across many screens.

### Examples

```
/design-dna:build a settings screen from ./tokens.css
/design-dna:build the charging-status card — reuse the existing tokens, don't re-extract
/design-dna:build an empty-state for the history list using our design system
```

> Need to extract the system first? Start with `/design-dna:create`. Just checking a
> rebuild's fidelity? Use `/design-dna:verify`.
