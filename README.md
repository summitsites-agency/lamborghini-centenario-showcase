# Centenario — Scroll Showcase

A single-page, monochrome "luminous studio" showcase for the Lamborghini Centenario,
built around a **scroll-linked image sequence** (the Apple AirPods technique) plus a
parallax hero, a sticky-scroll reveal, and springy hover cards. Design demo by Summit Sites.

## Drop-in usage

Copy these three items to your site and open `index.html` (must be served over http,
not `file://`, because the frames are fetched):

```
index.html        ← self-contained page (all CSS + JS inline)
frames/           ← 192 JPG frames (frame-0001.jpg … frame-0192.jpg) — the scroll sequence
images/           ← 4 high-res studio stills used in the hero, reveal & cards
```

Quick local preview:

```bash
python -m http.server 8080   # then visit http://localhost:8080
```

Dependencies load from CDN (no build step): **GSAP 3.12**, **ScrollTrigger**, **Lenis 1.1**.

## What's implemented (per `scroll animation.txt`)

1. **Scroll-linked canvas sequence** — 192 frames preloaded, scroll mapped to frame index,
   canvas **pinned** while it plays, **scrubbed** smoothly (GSAP `scrub`), DPR-aware and
   centered so it stays sharp on mobile, with a **loading progress fallback**.
2. **Parallax hero** — background wordmark, midground car still, and headline move at three
   different speeds for depth; subtle and clean on mobile.
3. **Sticky-scroll reveal** — the visual stays pinned on the right (crossfading between
   stills) while three copy blocks scroll past on the left, each fading/highlighting when
   active; collapses to a single column on mobile.
4. **Hover cards** — lift + growing shadow + image zoom + CTA fade, timed with GSAP
   (springy `back.out`); respects `prefers-reduced-motion` and gives touch devices a tap state.

Performance: the canvas only repaints when the frame index changes and there are no
continuous glow/blend effects → a measured **60fps / 0 long frames** while scrubbing.

## Assets & how they were made

- **`frames/`** were re-extracted from `Car_rotation_intact_to_expanded_*.mp4` at native
  1280×720 (sharper than the ezgif zip, which was double-compressed + interpolated), and the
  small "Veo" corner watermark was inpainted out. Swap in a higher-resolution frame set at the
  same filenames (`frame-0001.jpg …`) and update `FRAME_COUNT` in `index.html` if the count changes.
- **`images/`** are web-optimized (2000px) versions of the supplied 2K studio stills.
- The CSS studio-gradient tokens were sampled from the real frames so the canvas blends
  edge-to-edge with the page (no visible rectangle).

Source files kept in this folder (`*.mp4`, `*.jpeg`, `ezgif-*.zip`, `scroll animation.txt`)
are the originals and are **not** required to run the site.

## Disclaimer

Fictional design demonstration and homage — not affiliated with, endorsed by, or produced by
Automobili Lamborghini S.p.A. All imagery is illustrative.
