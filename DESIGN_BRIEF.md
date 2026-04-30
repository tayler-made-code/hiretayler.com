# Design brief — hiretayler.com color redesign

This document is for a fresh Claude session (or any designer) walking in cold to redesign the **color palette only**. Type system, copy, layout, and animation behavior are locked. The goal is to swap the palette without losing the personality.

---

## Who this site is for

A hiring manager evaluating Tayler Coon, a full-stack engineer who came up through Help Desk and Atlas School and is now actively looking for product engineering work. The site is the entire pitch — there's no separate cover letter.

## Voice — the energy you're protecting

The copy was hard-fought. It's first-person, NEPQ / Hormozi-direct, warm, slightly self-aware. Examples to feel:

- Hero: **"I build [tools/apps/sites/products/things] I wish existed. *Yours next?*"**
  - Italic, accent-colored "Yours next?" delivers the punch.
- About H2: **"A full-stack engineer drawn to *problems worth solving.*"**
  - Italic, accent-colored "problems worth solving" carries the thesis.
- Sidebar: **"Work I'd tell my friends about, with people I'd meet for a beer."**
- Contact: **"Looking for someone who actually builds?"** + **"I'm checking my email. Probably right now."**
- Available pill (top of page, with pulsing dot): **"Currently available for hire"**
- Disabled-form fallback: **"The tailor's out at lunch. In the meantime, just email me…"**

What it is NOT: corporate, cold, "shipping as the point" industry-cosplay, ironic, mono-only terminal aesthetic, dark-mode tech-bro. The previous direction was terminal/brutalist; the user explicitly rejected it for being a borrowed identity. Whatever palette comes next has to feel **earnest, warm, confident without bragging**.

---

## What's locked (don't touch)

- **Typography:** Space Grotesk (display, weights 400-700) + Inter (body) + Instrument Serif italic (accent words). All from Google Fonts. Italic Instrument Serif is the signature emphasis treatment.
- **Copy.** Every line was iterated to a sign-off. Don't rephrase.
- **Layout:** hero → bauhaus rule → about (2-col with sidebar) → bauhaus rule → work grid (3-col `ProjectCard`s) → contact (rounded inverted block) → tailor form section → footer.
- **Animations:**
  - Favicon: 2s cosine-eased opacity pulse 1.0 → 0.5 → 1.0 (matches the "available" header pill).
  - Header pill: solid dot pulses via Tailwind `animate-pulse`.
  - Hero noun: rotates through `['tools', 'apps', 'sites', 'products', 'things']`.
  - Project cards (`.pocket`): on hover, background swaps to accent color with a polka-dot lining pattern; text inverts.
  - "Silly sock" wiggle: one element on the page wiggles every ~5.5s. Honors `prefers-reduced-motion`.
  - `rotate-in` page-load animation, staircased delays.
- **Patterns / textures:**
  - Subtle SVG grain overlay on `body` (4% opacity, multiply blend) — the warmth comes from this as much as from color.
  - Polka-dot lining motif inside hovered project cards and at the page-bottom "exposed hem" section.
  - Hard 3px horizontal rules between major sections (Bauhaus-style).

---

## Current palette (the thing being replaced)

Internally nicknamed the **"utensil pot"** palette: warm cream + white outside, red-orange + teal inside, like a Le Creuset Dutch oven.

| Token | Hex | Role |
|---|---|---|
| `--color-bg` | `#f4f1ea` | Warm cream page background |
| `--color-paper` | `#ffffff` | Pure white card surface |
| `--color-ink` | `#0a0a0a` | Near-black type |
| `--color-dim` | `#6b6b6b` | Secondary text |
| `--color-red` | `#d94a34` | Primary accent — italic words, dot, CTAs, hovered cards (variant A) |
| `--color-red-deep` | `#a83420` | Hover/pressed state for red |
| `--color-teal` | `#3fa4b5` | Secondary accent — section labels ("ABOUT", "WORK"), hovered cards (variant B), underlines |
| `--color-teal-deep` | `#1f7d8e` | Hover/pressed state for teal |
| `--color-rule` | `#1a1a1a` | Hard black rules, card borders, button strokes |

The palette appears in `src/styles/global.css` as `@theme` CSS variables (Tailwind v4 syntax). Components reference them via `bg-[var(--color-red)]`, `text-[var(--color-teal)]`, etc., and a few inline `style="color: var(...)"` blocks for the italic accent words.

### Where each color fires (so a redesign keeps the rhythm)

- **Background hierarchy:** page (`--color-bg`) → cards (`--color-paper`) → contact section (inverted, dark `--color-ink`). Three tiers of "depth."
- **Italic accent word color** = `--color-red`. Appears in: hero rotating noun, About H2 ("problems worth solving"), "Yours next?", "shipping" and "Hire me" inline accents. This is the highest-value pixel on the page — wherever red lands, the eye lands.
- **Section labels** (eyebrow text above each H2: "ABOUT", "WORK", "WHAT I'M AFTER", "TAILOR YOUR RÉSUMÉ") = `--color-teal`. Bold, uppercase, tracked-out.
- **Available pill dot, contact section "looking for X"** = red.
- **Project card hovers:** half use red lining, half use teal lining (`pocket--teal` variant), creating visual variety down the grid.
- **Contact section** (inverted): dark ink background with a red and a teal blurred radial gradient bleeding in from corners. The two accents meet here as ambient glow.
- **Tailor form fields:** white paper on cream, red focus ring.

---

## What's open for redesign

**Just the palette.** Roles stay the same — the redesign needs to define new tokens that play those roles. Specifically:

1. **Page background** — currently warm cream. Could go cooler, darker, more saturated, or remain off-white but in a different undertone. Whatever it is, the SVG grain still rides on top.
2. **Card surface** — currently pure white. Could shift if the page background changes.
3. **Type ink + dim** — currently near-black + medium-gray. Open to a softer ink (charcoal, deep blue-black, etc.) but it must hold contrast for body copy at 16-18px.
4. **Primary accent** — currently red-orange. This is the pulse dot, italic emphasis word, primary CTA. It needs to read confidently, warmly, not corporate-blue.
5. **Secondary accent** — currently teal. This carries section labels and the alternate card-hover variant. It needs to harmonize with the primary accent without competing.
6. **Hard-rule color** — currently near-black. Could match the new ink, could go bolder.
7. **Hover lining pattern color** — currently white-on-accent polka dots. The dots themselves can recolor; the pattern stays.

The two-accent system is structural. Don't collapse to one accent unless you have a strong replacement for the rhythm.

---

## Constraints

- **Contrast.** Body copy (16-18px Inter) on the new background must clear WCAG AA (4.5:1). Section labels at 12px/uppercase need AA at small text (4.5:1). Italic accent words can flex slightly but should remain readable.
- **The pulse dot must read as "alive."** The accent color paired with the page background needs to support a 50% opacity pulse without disappearing.
- **Pocket-hover animation depends on the accent contrasting with white text** layered over it. Whatever the new accent is, white type must hold AA on top of it.
- **OG image (`public/og.png`) currently bakes in `#d94a34`.** A regen will be needed once the new palette lands. The favicon SVG (`public/favicon.svg`) hardcodes the same red and the inline canvas script in `src/layouts/Base.astro` hardcodes `#d94a34` — these three places need a coordinated swap.

---

## Direction prompts (optional)

The user is open to vibe directions, not committed to one. Some prompts a designer-Claude could explore:

- **"Field notebook":** ink, cream, a single warm accent (rust, ochre, oxidized brass). Drop teal. Lean Wes-Anderson-meets-engineer's-journal.
- **"Gallery wall":** off-white, charcoal, two saturated accents that sit inside a curated palette (e.g., cobalt + persimmon, or oxblood + sage). Editorial, museum-coded.
- **"Dawn":** softly desaturated peach-cream background, deep navy ink, warm amber primary accent, dusty sage secondary. Calm, optimistic.
- **"Workshop":** putty/concrete background, near-black ink, electric primary (signal yellow or alarm red), muted secondary. Industrial-cool but not cold.
- **"Stay close, swap heat":** keep the cream/paper/ink trio almost identical, change ONLY the two accents. Lowest-risk redesign — preserves the warmth while refreshing the signature italic-word color and the section labels.

The user wants **earnest, warm, confident**. Avoid: hyper-corporate blue, neon, full dark mode, high-contrast tech-bro, terminal-green-on-black.

---

## Files to touch

- `src/styles/global.css` — `@theme` block with `--color-*` tokens. Change values here.
- `public/favicon.svg` — replace `fill="#d94a34"` with new accent.
- `src/layouts/Base.astro` — inline canvas script has `ctx.fillStyle = '#d94a34'`. Update.
- `public/og.png` — regenerate after palette is decided. Source HTML lives in this repo's history (last regen was via Chrome headless from an inline HTML template); regenerate with the new accent and crop to 1200x630.
- A few inline `style="color: var(--color-red)"` blocks in `src/pages/index.astro` — these reference the CSS variable, so they'll pick up the new palette automatically. Don't refactor.

---

## Definition of done

- New `@theme` tokens in place; existing CSS variable references unchanged.
- Favicon and Base.astro canvas script color updated.
- New OG image generated and saved at `public/og.png` (1200x630 PNG).
- Visual sanity-check across: hero, About, work grid (with one card hovered to verify lining contrast), contact section, tailor form, footer.
- Lighthouse contrast audit clean.
- The site still feels like Tayler — earnest, warm, confident — not like a different person wearing his clothes.
