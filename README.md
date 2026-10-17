# Solarpunk Waterfront — Pixel Art Comparison

Two interpretations of the same prompt: an animated 16-bit pixel-art solarpunk city
waterfront with glass domes, cascading greenery, rooftop wind turbines, airships,
tiered waterfalls, a turning water wheel, a lookout dock and solar-powered boats.

![Side-by-side comparison](media/comparison.gif)

*Left: Gemini 4 Argon (high). Right: Grok 4.6, the build in this repo.*

## The prompt

> Create an animated pixel-art illustration of a vibrant solarpunk city waterfront:
> glass-domed towers covered in cascading greenery and vines, futuristic wind
> turbines on the rooftops, airships drifting in the sky, multi-tiered waterfalls
> spilling into a canal, a large wooden water wheel turning, a lookout dock, and
> solar-powered wooden boats. Isometric-ish 16-bit pixel art, Studio Ghibli color
> palette, highly detailed, cozy, serene, warm.

## Results at a glance

| | Gemini 4 Argon (high) | Grok 4.6 (this repo) |
|---|---|---|
| Output | Pre-rendered MP4 video + poster | Single self-contained HTML canvas |
| Resolution | 1080 × 720 | 480 × 270, integer-scaled to any viewport |
| Frame rate / loop | 12.5 fps, 3.84 s loop | 60 fps, continuous |
| Rendering | AI-generated video frames | Procedural 2D canvas drawing |
| Assets | `solarpunk-city.mp4`, `poster.png` | None — all geometry and color are code |
| Download size | 1.86 MB video | 75 KB HTML |
| Session time | ~13 min | 20 min |
| Cost | $1.20 (Devin desktop, 75% Argon promo) | 8.2M tokens |
| Interactivity | Video playback only | Live scene, resizes to the window |
| Source of motion | Generated pixels; loops back to start | Deterministic per-pixel animation, no loop seam |

Gemini reference: https://gemini-4-argon.vercel.app/tests/gemini-4-argon-high-solarpunk-city/index.html

## What the comparison shows

**Gemini 4 Argon** produced a dense, unified night scene. The strongest part is
architectural composition: the long arched viaduct, varied rooflines, crowds of
lit windows and the mosaic-like foliage all read as one illustration. Its motion
is subtle — water shimmer, waterfall flow, turbine blades — and is baked into a
short video. It is a finished picture first and an animation second.

**Grok 4.6** produced a lighter, more open daytime scene drawn entirely at runtime.
The camera is wider, so individual props (mill, wheel, dock, boats, tiered pools)
get more breathing room but less architectural density. Every animated element is
parameterized by time: clouds drift and wrap, airships bob, turbine rotors turn at
different phases, water highlights shimmer, the water wheel rotates, boats bob, and
lanterns flicker. Because it is canvas output, it stays crisp at any integer scale
and responds to window resize, but it can never match the frame-level texture
density of a generated 1080p video.

### Feature checklist

| Feature | Gemini | Grok 4.6 |
|---|---|---|
| Glass domes | Yes, multiple, mosaic-textured | Yes, two large domes with internal vine lattices |
| Cascading greenery / vines | Dense, covering facades | Hanging vines on towers, dome skirts, bridges |
| Rooftop wind turbines | Yes, several incl. skyline | Yes, four rooftop turbines with animated rotors |
| Airships | Yes, small, numerous | Yes, three detailed airships with solar tops |
| Multi-tiered waterfall | Single tall fall through arches | Three elliptical pools with stepped falls into canal |
| Wooden water wheel | Yes, integrated into a building | Yes, 10-spoke wheel with paddles, splash and foam |
| Lookout dock | Foreground pier with figures | Elevated lookout tower, ladder, deck, cat, crates |
| Solar-powered boats | Yes, small boats on canal | Rowboat, solar-canopy boat, distant skiff |
| Responsive / scalable | Letterboxed video | Integer-scaled canvas, resizes live |

## Individual loops

| Gemini 4 Argon | Grok 4.6 |
|---|---|
| ![Gemini loop](media/gemini-scene.gif) | ![Grok loop](media/grok46-scene.gif) |

## Repo layout

```
index.html               Grok 4.6 scene (single file, no dependencies)
media/comparison.gif     Side-by-side animated comparison
media/comparison.png     Still frame of the comparison
media/gemini-scene.gif   Gemini loop, re-encoded from its MP4
media/grok46-scene.gif   Grok 4.6 loop, captured from the canvas
```

## Run it

Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Notes on methodology

- The Grok frames were captured from the live canvas at 8 fps and assembled into
  the comparison GIF; the scene itself renders at 60 fps in the browser.
- The Gemini loop was decoded from the published 12.5 fps MP4 and re-sampled to
  the same frame count so both panels advance together.
- Timing and cost figures come from the original test notes: Gemini on the Devin
  desktop app with the 75% Argon promo; Grok 4.6 at 20 minutes and 8.2M tokens.
