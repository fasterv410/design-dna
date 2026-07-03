---
trigger: model_decision
description: Reverse-engineer a design system from a reference image — measure real pixels, build semantic tokens, rebuild in a lab, verify by measurement.
---

# Design DNA (Windsurf rule)

Install: copy this file to `.windsurf/rules/design-dna.md` in your project.
Windsurf's Cascade applies it when the task matches the description
(`trigger: model_decision`), or set `trigger: always_on` to keep it active.

## The one rule

**Measure, don't guess.** Sample real pixels. Never type a hex code or a size
from memory.

## The method — seven steps, in order

1. **Capture** — references at full resolution; note the device scale (3x
   phone: 1320px file = 440pt) to convert pixels to layout units.
2. **Measure** — exact colors (crop + eyedropper), type sizes (cap-height px ÷
   scale), spacing, radii, shadows. Record real numbers.
3. **Distill** — write `REFERENCE.md`: palette with semantic roles, type scale,
   spacing/radius law, depth model, 3–6 named principles, and a name.
4. **Tokenize** — raw primitives + semantic roles named by role. Data-viz
   colors are semantic to the data, used only on data ink. Light + dark as
   parallel sets if needed.
5. **Lab** — rebuild a 1:1 replica in an isolated sandbox using only the
   tokens. A missing token is a gap to add. Lab shortcuts never leak to
   production.
6. **Verify** — measure the rebuild vs the reference with
   `getBoundingClientRect` and computed-color sampling. Threshold: 1–3px on
   geometry, exact on color. Trust the number over your eye.
7. **Record** — write an ADR (supersede, don't delete), then promote from lab
   to production.

## Ethics

Extract the *system* and rebuild it as your own original work. Don't republish
the reference's assets or branding.
