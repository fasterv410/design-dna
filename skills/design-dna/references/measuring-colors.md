# Measuring colors and sizes from an image

The point of this file: never type a hex code from memory. Pull it from a pixel.

## macOS (built-in, no installs) — `sips`

`sips` ships with every Mac. Use it to crop a flat region, then read its color.

### 1. Crop a region you know is one flat color

```bash
# crop a 20x20 swatch starting near the top-left of a card surface
sips -c 20 20 --cropOffset 40 300 reference.png --out /tmp/swatch.png
#      │  │                  │   │
#      │  └ width            │   └ y offset (px from top)
#      └ height              └ x offset (px from left)
```

Adjust the offsets so the crop lands inside a solid area (a card, the canvas,
a text glyph, an accent chip) with no edges or gradients.

### 2. Read the color out of the crop

`sips` can't print a pixel value directly, so downsample the swatch to a single
pixel and read it. Two easy ways:

```bash
# Option A: macOS Digital Color Meter (GUI) — hover the crop, it shows hex.

# Option B: shrink to 1x1 and dump the pixel with Python (ships with macOS)
sips -z 1 1 /tmp/swatch.png --out /tmp/px.png
python3 - <<'PY'
from PIL import Image      # pip install pillow, or use the snippet below
print('#%02X%02X%02X' % Image.open('/tmp/px.png').convert('RGB').getpixel((0,0)))
PY
```

No Pillow? Use `sips` to average and screen-read, or use the DevTools eyedropper
in any browser by opening the image in a tab.

### 3. Browser eyedropper (any OS)

Open the reference image in a browser tab and use the built-in eyedropper:

- Chrome/Edge DevTools → Elements → any color swatch → the eyedropper picks any
  on-screen pixel and reports exact hex.
- Firefox → the eyedropper tool (Tools → Browser Tools → Eyedropper).

## Converting pixels to layout units

Screenshots from phones are scaled. Convert measured pixels to real units:

```
layout_unit = measured_pixels / device_scale
```

- iPhone (3x): a 1320px-wide file is 440pt wide. A glyph 84px tall ≈ 28pt.
- iPhone (2x) / many Android: divide by 2.
- Desktop screenshots at 1x: pixels are already close to CSS px (watch for
  Retina 2x captures).

Always find one known dimension (screen width) to confirm the scale before
trusting the rest.

## What to measure

| Property     | How                                                            |
|--------------|---------------------------------------------------------------|
| Surface hex  | Crop a flat area of each surface: canvas, card, sunken well.   |
| Text hex     | Crop over a bold glyph; sample the darkest interior pixel.     |
| Accent hex   | Crop the brightest saturated element (button, active state).   |
| Type size    | Cap-height in px ÷ device scale.                               |
| Line gap     | Baseline-to-baseline in px ÷ device scale.                     |
| Padding      | Edge-of-content to edge-of-card in px ÷ device scale.          |
| Radius       | Fit a circle to a corner; its radius in px ÷ device scale.     |
| Shadow       | Note color, blur softness, vertical offset, spread by eye+crop.|

## Turning measurements into a token table

Record every value with a role, e.g.:

```
canvas       #F7F7FB   page background
card         #FFFFFF   raised surface
sunken       #F0F0F3   inset well / track
ink          #222325   primary text
muted-ink    #8A8A90   secondary text
accent       #6B5CFF   single loud action / active
viz-good     #38C79A   data ink only — "healthy"
viz-warn     #E7B549   data ink only — "caution"
```

Keep raw hex now; convert to `oklch()` later if desired — the conversion does
not change what renders, so fidelity is preserved.
