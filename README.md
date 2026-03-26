# Pillar Wallpaper Creator

A browser-based wallpaper design tool. Build wallpapers made of overlapping rounded rectangles ("pillars") and export them as a PNG at up to 8K resolution. Runs entirely client-side — no build step, no backend, no dependencies. Open `index.html` and start designing.

## Getting started

Download or clone the repo, then open `index.html` in any modern browser. No installation required.

## Layout

The interface is a three-column layout with a topbar:

- **Left panel** — canvas settings, pillar count, stack order, and presets
- **Center** — live canvas preview
- **Right panel** — per-pillar color swatches and shape controls

---

## Features

### Canvas ratio

Choose from five aspect ratios. The preview canvas resizes to match and the export resolution label updates automatically.

| Ratio | Export resolution |
|-------|------------------|
| 16:9  | 7680 × 4320 px   |
| 4:3   | 5760 × 4320 px   |
| 1:1   | 4320 × 4320 px   |
| 21:9  | 7560 × 3240 px   |
| 9:16  | 4320 × 7680 px   |

### Background color

Click the background swatch to open a color picker. The hex value is displayed alongside the swatch and updates live.

### Pillar count

A slider controls how many pillars are rendered, from 3 to 12. Adding pillars inherits the color of the last existing pillar. Removing pillars trims from the right.

### Stack order

Toggle which end of the pillar group sits on top:

- **Right on top** (default) — the rightmost pillar is fully visible, earlier pillars peek out to the left
- **Left on top** — the leftmost pillar is fully visible, later pillars peek out to the right

### Reverse color order

Click **Reverse Color Order** (below the stack order toggle) to flip the pillar color array. This reverses the gradient direction without changing the stack order.

### Orientation

Switch between horizontal and vertical pillar stacking:

- **Horizontal** (default) — pillars are arranged side by side, left to right. Defaults the canvas ratio to 16:9.
- **Vertical** — pillars are stacked top to bottom, ideal for mobile/portrait wallpapers. Defaults the canvas ratio to 9:16.

### Presets

30 built-in presets organised into four groups. Clicking a preset sets the background color and all pillar colors at once.

**Classic** — warm, natural palettes with tinted backgrounds
- Autumn, Ocean, Forest, Rose, Dusk

**Light** — vivid color progressions on a white background
- Citrus, Berry, Mint, Sky, Lavender, Coral, Teal, Amber, Spectrum, Graphite

**Dark** — luminous colors on a near-black background
- Ember, Neon, Ice, Venom, Violet, Plasma, Crimson, Aurora, Cobalt, Steel

**Pastel** — soft, high-lightness palettes on a near-white background
- Blush, Mint, Powder, Peach, Lilac

### Randomize

Click **Randomize** (below the presets grid) to generate a themed palette. Each click picks a random color harmony strategy — monochrome, analogous, complementary, triadic, or split-complementary — and produces a cohesive set of pillar colors with a matching background. The theme can be light or dark.

### Per-pillar colors

The right panel shows a color swatch for every active pillar, numbered left to right. Click any swatch to open a color picker for that pillar. You can also click directly on a pillar in the canvas preview — the topmost pillar at that position is selected.

### Shape controls

All shape parameters are in the right panel and update the preview in real time.

| Slider    | What it controls                                              | Range   | Default |
|-----------|---------------------------------------------------------------|---------|---------|
| Roundness | Border radius as a percentage of half the pillar width        | 0–100   | 100     |
| Width     | Pillar width as a percentage of the canvas width              | 10–80   | 15      |
| Height    | Pillar height as a percentage of the canvas height            | 40–100  | 70      |
| Overlap   | How much each pillar overlaps the previous, as a % of its width | 0–80  | 55      |
| Shade     | Depth shadow on the overlap edge of each pillar               | 0–100   | 0       |

**Shade** renders a dark-to-transparent gradient on the overlap edge of each pillar, clipped to its rounded shape. This adds a sense of depth and separation between layers. The gradient direction follows the stack order — left edge for right-on-top, right edge for left-on-top.

---

## Exporting

### Export 8K PNG

Click **Export 8K** in the topbar. The app renders the design at full export resolution (up to 7680 × 4320 px depending on the selected ratio) and downloads a PNG file named `wallpaper-8k.png`.

PNG is used because the image is purely geometric — lossless compression means no artefacts on pillar edges or flat backgrounds, and the file size stays manageable due to large areas of solid color.

### Export Config

Click **Export Config** to download the current design as a JSON file (`wallpaper-config.json`). The file captures all state: ratio, background color, pillar count, pillar colors, all shape slider values, stack order, and orientation.

### Import Config

Click **Import Config** to load a previously exported config file. Unknown or missing fields are ignored, so partial configs are safe to import.

Example config file:

```json
{
  "ratio": "16:9",
  "bgColor": "#F2EDDF",
  "pillarCount": 10,
  "pillarColors": [
    "#F5C842", "#F0A830", "#E8862A", "#D96628", "#C94E22",
    "#B83A20", "#9B2A1C", "#7C1E18", "#4A1010", "#2A0808"
  ],
  "roundness": 100,
  "pillarWidthPct": 15,
  "pillarHeightPct": 70,
  "overlapPct": 55,
  "shadePct": 0,
  "stackReversed": false,
  "flipped": false
}
```

### Reset

Click **Reset** in the topbar to restore all settings to their defaults (Autumn preset, 16:9 ratio, default slider values).
