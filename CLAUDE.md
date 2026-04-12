# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static personal portfolio website for **Muhammad Abdullah Khan** — AI Automation Builder (n8n · RAG · Voice AI · WhatsApp Automation · PharmD). No build tools, no dependencies beyond Google Fonts CDN. Opens directly in a browser.

## File Structure

```
/
├── index.html          # Homepage — all sections in one file
├── pricing.html        # Pricing tiers (Audit / Single System / Full Stack)
├── faq.html            # FAQ accordion + contact form (14 questions, filterable)
├── CLAUDE.md           # This file
├── Portfolio/
│   ├── assets-brief.md # Image/video generation prompts with aspect ratios
│   └── files/          # ALL media assets (images + video)
│       ├── *.jpeg/png  # Section backgrounds, service icons, profile photo
│       └── *.mp4       # Hero background video loop
└── refernces/          # Reference screenshots (design inspiration)
```

**Critical:** All media is in `Portfolio/files/`. Paths in HTML must use `Portfolio/files/<filename>`. Do not move files without updating all three HTML files.

## Architecture

Each HTML file is fully self-contained — all CSS and JS inline, no external files except Google Fonts. The three pages share identical design tokens, nav, footer, animations, and JS patterns but are not templated; changes to shared elements must be applied to all three files manually.

**CSS structure inside each file:** Single `<style>` block, sections commented with `/* ── NAME ── */` following DOM order. Design tokens in `:root`.

**JS at bottom of each file handles:**
- `IntersectionObserver` scroll reveal (`.reveal` + `.reveal-delay-1` through `6`)
- Animated counters on `[data-count]` / `[data-suffix]` attributes (index.html only)
- Scroll spy — `[data-section]` on nav `<a>` tags, toggles `.active` (index.html only)
- Lightbox — `#openLightbox` → `#lightbox` overlay, closes on Esc / backdrop (index.html only)
- FAQ accordion — expand/collapse + category filter buttons (faq.html only)
- Contact form — frontend validation + simulated submit with success state (faq.html only)
- Hamburger / back-to-top — class toggles on all pages

## Design Tokens

| Token | Value | Use |
|---|---|---|
| `--bg` | `#05050d` | Page background |
| `--bg2` | `#0d0d18` | Card surface |
| `--bg3` | `#151520` | Inset / icon background |
| `--accent` | `#7c6fff` | Primary purple |
| `--accent2` | `#b39dff` | Gradient start, lighter purple |
| `--accent3` | `#e879f9` | Gradient end, fuchsia |
| `--border` | `#1e1e30` | All borders |
| `--muted` | `#777799` | Secondary text |

`.gradient-text` — animated shimmer gradient applied to inline text.  
`.btn-wa` — green WhatsApp button style (distinct from purple `.btn`).

## Key Conventions

**Responsive breakpoints (same on all pages):**
- `< 1024px` — services/testimonials 3→2 col
- `< 900px` — about grid stacks, featured box stacks
- `< 768px` — mobile: hamburger shows, nav links hide, all grids 1 col
- `< 480px` — h1 font size reduction

**Reveal pattern:** Add `class="reveal"` + optionally `reveal-delay-1` to `reveal-delay-6`. The IntersectionObserver fires `.visible` on entry.

**Animated counters:** `data-count="100"` + `data-suffix="%"` on any `.stat-number` element.

**Section IDs for scroll spy:** `about`, `services`, `process`, `system`, `testimonials`, `contact` — must match `data-section` on nav links.

**Nav structure:** Main anchors → `<span class="nav-divider">` → `pricing.html` / `faq.html` → `<span class="nav-divider">` → `.nav-cta` Book Audit button.

**WhatsApp link:** `https://wa.me/92326281281` — used in hero CTAs, contact section, footer, pricing page, faq page.

## Pages Summary

| Page | Key sections |
|---|---|
| `index.html` | Hero (video bg) · Tools marquee · About (photo+stats) · Services (6 cards) · Process · Featured System (lightbox) · Testimonials · Contact |
| `pricing.html` | Hero · 3 pricing tiers · FAQ strip · Bottom CTA |
| `faq.html` | Hero · Filterable accordion (14 Qs, 4 categories) · Contact form · Bottom CTA |

## What Still Needs Real Content

- **Profile photo** — `new pics and videos/relacreplace_background_to_202604121250.png` (real DP, already wired)
- **Testimonials** — three placeholder cards in `index.html #testimonials`; replace `.testi-body`, `.testi-name`, `.testi-role`
- **Booking link** — all CTAs point to LinkedIn; replace with Cal.com link when available
- **Contact form** — `faq.html` form is frontend-only; wire the `fetch()` call to Formspree / Make / n8n webhook
- **Pricing figures** — `$1,500` and `$4,000` are placeholders; update to real numbers

## Deployment (Vercel)

Before pushing to GitHub / deploying to Vercel:
1. Verify all image paths use `Portfolio/files/` prefix
2. Confirm `Portfolio/files/` folder is committed (it contains large files — check `.gitignore`)
3. Entry point is `index.html` at root — Vercel auto-detects this as a static site, no config needed
