# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Professional personal portfolio website for **Muhammad Abdullah Khan** — AI Automation Builder. Features a robust **Light/Dark Mode** system, mobile-optimized animations, and localized content for AI agency services. Built with pure HTML/CSS/JS (no build tools).

## File Structure

```
/
├── index.html          # Homepage — Hero, Services, ROI, Testimonials, Contact
├── pricing.html        # Pricing tiers & simple FAQ strip
├── faq.html            # Deep FAQ accordion + contact form
├── notes.html          # Build Notes / Case Study detail page
├── Portfolio/
│   ├── assets-brief.md # Prompts used for media generation
│   └── files/          # ALL media assets (images + video)
│       ├── *.jpeg/png  # Backgrounds, Icons, Profile Photo
│       └── *.mp4       # Hero background video
```

**Critical:** All media is in `Portfolio/files/`. Paths in HTML must use `Portfolio/files/<filename>`.

## Architecture

Pages are self-contained (all CSS/JS inline). Design tokens, nav, and footer are shared across all 4 pages.

**Theme System:**
- Uses `html[data-theme="light"]` attribute.
- Tokens defined in `:root` (dark) and `html[data-theme="light"]` (light).
- JavaScript at the bottom of each file handles persistence via `localStorage`.
- **Visibility Fix:** Sub-pages use explicit light-mode CSS overrides (`color: #1a1a24 !important`) to ensure visibility where variable inheritance is flaky.

**JavaScript Features:**
- `IntersectionObserver` Scroll Reveal: Adds `.visible` to `.reveal` elements.
- **Mobile Fallback:** Every page has a 2.5s timeout that forces visibility if the observer fails to trigger on mobile (`revealAllFallback()`).
- ROI Calculator: Handles monthly savings logic (index.html).
- Chatbot: Fully themed AI qualification agent (index.html).
- Smooth Scroll: Handled via `scroll-behavior: smooth` and scroll-spy for active nav states.

## Design Tokens

| Token | Dark (Default) | Light (`data-theme="light"`) |
|---|---|---|
| `--bg` | `#05050d` | `#fafafa` |
| `--bg2` | `#0d0d18` | `#ffffff` |
| `--bg3` | `#151520` | `#f0f0f5` |
| `--accent` | `#7c6fff` | `#5e4bd8` |
| `--accent2` | `#b39dff` | `#7c6fff` |
| `--text` | `#eeeeff` | `#1a1a24` |
| `--muted` | `#777799` | `#6a6a8a` |
| `--border` | `#1e1e30` | `#e2e2ec` |

## Key Conventions

**Mobile Responsive Breakpoints:**
- `< 1024px` — 3→2 column transitions
- `< 768px` — Mobile view: hamburger menu, single-column stacks
- `< 480px` — H1 scaling and padding reductions

**Reveal Pattern:**
- Use `class="reveal"` with `reveal-delay-1` through `6`.
- Animations trigger when 10% of element is visible.

**Theme Toggle:**
- Handled by `#themeToggle`. Switches icons between `#moonIcon` and `#sunIcon`.

## Pages Summary

| Page | Key Features |
|---|---|
| `index.html` | Hero Video · Auto-Marquee · ROI Calc · Testimonials · Chatbot |
| `pricing.html` | 3 Pricing tiers (Audit, System, Stack) · FAQ Strip |
| `faq.html` | Filterable 14-question accordion · Advanced Contact Form |
| `notes.html` | Case Study (Problem, Arch, Results) · Light-mode optimized |

## Content Readiness

- **Profile photo** — Live (Portrait photo in about section)
- **Booking link** — Cal.com link is active across all CTAs
- **Testimonials** — Placeholders still exist; need real client names/quotes.
- **WhatsApp** — Live (`+92326281281`)

## Deployment (Vercel)

1. Verify paths are strictly `Portfolio/files/`.
2. Ensure large media files are not ignored by `.vercelignore`.
3. Entry point is `index.html`. Vercel auto-deploys on push to `master`.
