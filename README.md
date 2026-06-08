# KC3EFJ

Source for [**kc3efj.net**](https://kc3efj.net) — the personal site of **Jeff Hopkins (KC3EFJ)**, an amateur radio operator in Port St. John (Cocoa), Florida. Interests include digital modes, APRS, Meshtastic, and Eurorack.

It's a static, dependency-free site: hand-written HTML/CSS/JS with all rendering done in WebGL. There is no build step and there are no third-party libraries or CDN includes — every file can be opened directly in a browser.

## Pages

### `index.html` — Landing page

The home page. A glowing neon **KC3EFJ** callsign sits over a full-screen animated particle network rendered in **WebGL**:

- ~150 nodes drift around the canvas, drawing glowing links to nearby neighbors and to the mouse/touch cursor.
- Clicking a node triggers a cascading "flood fill" signal that propagates through the network like a digital transmission spreading across the mesh.
- Clicking the callsign smoothly reveals a short bio blurb with contact details.
- Custom GLSL vertex/fragment shaders render the nodes as anti-aliased SDF circles and the connections as glowing lines.
- Dark synthwave palette (cyan/magenta on deep blue), monospace type, responsive down to mobile, and installable as a PWA (Apple web-app meta tags, theme color).

**Contact:** `contact@kc3efj.net` · [github.com/jeffmhopkins](https://github.com/jeffmhopkins/)

### `tron-demo.html` — "OUTRUN GRID" synthwave/Tron CRT demo

A standalone, more elaborate **WebGL 2** demo: a first-person flight through a neon grid world, finished with a CRT post-processing pipeline. Self-contained in a single ~1,260-line file with hand-written GLSL ES 3.0 shaders and no frameworks.

What it renders:

- **Tron grid floor** — perspective-projected, scrolling, with a randomized heading so each load drifts a different direction toward the vanishing point.
- **Retro sun disc** — orange-to-magenta gradient with animated horizontal slits, sitting at the vanishing point.
- **Node network** — Brownian-motion nodes with dynamic links and signal pulses that cascade and branch along edges; nodes flee the cursor on hover.
- **Cameo objects** — shooting stars, a rare comet, tumbling wireframe polyhedra, light-cycle grid streaks, glyph clusters, and a distant horizon ridge, all on randomized timers.
- **Star Fox–style wingmate squadron** — 2–5 ships chosen from 5 wireframe models, fully 3D (roll/pitch/yaw), choreographed through approach → hold → peel-off phases with flickering engine glow and afterburner trails.

How it's built:

- **Multi-pass deferred rendering:** scene → bright-pass → separable Gaussian bloom → CRT composite.
- **CRT emulation** in the final shader: barrel distortion, chromatic aberration, scanlines, aperture grille, rolling band/flicker, film grain, and vignette.
- A single central `CONFIG` object exposes 45+ tunable parameters (speeds, spawn timings, colors, counts).
- Respects `prefers-reduced-motion` (renders a single static frame), pauses on hidden tabs, caps DPR and frame rate, reduces node count on mobile, and handles WebGL context loss/restore.

> Note: `tron-demo.html` is a standalone experiment — it is not linked from the landing page.

## Running locally

No build, no dependencies. Open either file directly in a modern browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/
```

A WebGL-capable browser is required (`index.html` uses WebGL 1; `tron-demo.html` uses WebGL 2, with a static fallback if unavailable).

## Deployment

The site is served as static files at the custom domain in [`CNAME`](CNAME) (`kc3efj.net`), suited to GitHub Pages or any static host.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Landing page with the WebGL callsign + particle network |
| `tron-demo.html` | Standalone "OUTRUN GRID" synthwave/Tron CRT WebGL 2 demo |
| `CNAME` | Custom domain (`kc3efj.net`) for static hosting |
