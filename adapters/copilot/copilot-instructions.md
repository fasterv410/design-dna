# Design DNA (GitHub Copilot instructions)

Install: copy this content into `.github/copilot-instructions.md` in your
project (create the file if it doesn't exist, or append this section).
GitHub Copilot reads it automatically for chat and edits in that repo.

---

## Design DNA method

When a task involves matching or learning from a visual reference (a
screenshot, app, or website), follow this method. **One rule above all:
measure, don't guess — sample real pixels, never type a hex or size from
memory.**

Seven steps, in order, each producing an artifact:

1. **Capture** — collect references at full resolution; note the device scale
   (3x phone: 1320px file = 440pt) to convert pixels to layout units.
2. **Measure** — exact colors (crop + eyedropper), type sizes (cap-height px ÷
   scale), spacing, radii, shadows. Record real numbers.
3. **Distill** — write `REFERENCE.md`: palette with semantic roles, type scale,
   spacing/radius law, depth model, 3–6 named principles, and a name for the
   direction.
4. **Tokenize** — two layers: raw primitives + semantic roles named by role
   (`--color-accent`, not `--color-purple`). Data-viz colors are semantic to
   the data, used only on data ink. Light + dark as parallel sets if needed.
5. **Lab** — rebuild a 1:1 replica in an isolated sandbox using only the
   tokens. A missing token is a gap to add. Lab shortcuts never leak to
   production.
6. **Verify** — measure the rebuild vs the reference with
   `getBoundingClientRect` and computed-color sampling. Threshold: within 1–3px
   on geometry, exact on color. Trust the number over your eye.
7. **Record** — write an ADR for the direction (supersede, don't delete), then
   promote the proven language from lab to production.

**Ethics:** extract the *system* and rebuild it as your own original work.
Don't republish the reference's assets or branding.
