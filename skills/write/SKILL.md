---
name: write
description: Use to write a high-converting, PREMIUM self-contained landing page (single index.html) from ./out/research.md — modern glassmorphism, gradient hero, niche-fit palette. Outputs ./out/site/index.html. Called as step 2 of the launch chain.
---

# write — research in, a real landing page out

1. Read `./out/research.md` (produced by the `research` skill).
2. Write ONE self-contained, responsive `./out/site/index.html` — no external files, inline CSS.

## Page structure (conversion order)

- **Hero** — headline from research's "winning angle" + subhead + primary CTA button.
- **The problem** — name the top pain from research (agitate briefly).
- **The offer** — what they get, in 3 benefit cards.
- **Proof strip** — a placeholder testimonial + trust line (mark `[replace]`).
- **Final CTA** — restate offer + button.
- Sticky-simple footer.

## Design bar — PREMIUM, not flat (this IS the demo)

Must look like a real agency-grade client site, not a template. Non-negotiable:

- **Rich background** — a dark `radial-gradient` with 1–2 blurred color "orbs", never a flat fill.
- **Hero** — oversized `clamp()` headline (900 weight, tight tracking) with a **gradient-text** accent word; a glass badge above; a primary gradient CTA + a ghost/glass secondary button.
- **Glassmorphism** stats/cards — `rgba(255,255,255,.06)` + `backdrop-filter:blur()` + subtle border; hover `translateY(-4px)`.
- **Inline stroked SVG icons** in feature cards (not emoji-only).
- Include: a **stat strip** (3 big numbers), a **testimonial** card with an avatar, a boxed **final CTA** band.
- `clamp()` type scale, generous spacing, mobile-first, obviously tappable buttons.

## Palette — fit the NICHE, not a fixed brand

Pick colors that suit the client (cold-plunge = deep navy/teal + icy cyan; law firm = ink + gold; etc.). Cohesive, high-contrast, one accent used through the gradients.

## Copy

Direct, founder-grade, **no fake stats** (mark proof as `[replace]`), never lorem. External hero image via a real URL is allowed (this deploys to Vercel, not a sandbox); a CSS-gradient hero is the safe premium default.

Save to `./out/site/index.html`. Do not deploy here — the `deploy` skill handles that. Stop after saving.
