# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Deployment

This is a static HTML/CSS/JS site hosted on GitHub Pages at **seanmaroney.com**.

To publish changes:
```bash
git add <files>
git commit -m "description"
git push origin main
```

GitHub Pages deploys automatically within 1–2 minutes of a push. The CNAME file maps the custom domain.

## Architecture

Two parallel versions of the site exist side by side:

- **`/` (root)** — the main styled version. Uses `style.css` and `nav.js`.
- **`/accessible/`** — a WCAG 2.2 AA compliant version with its own `style.css`. No `nav.js` (the accessible nav uses `flex-wrap` and needs no hamburger). Images are referenced as `../headshot4.png` (one level up).

The two versions are **not auto-synced** — content changes must be applied to both manually.

## Site structure

Five pages in each version: `index.html`, `research.html`, `publicphilosophy.html`, `cv.html`, `contact.html`.

Shared across the main version:
- `style.css` — all styling including a `@media (max-width: 768px)` block for mobile
- `nav.js` — hamburger menu toggle (included via `<script src="nav.js">` at bottom of each page)

## Design tokens (main version)

Defined as CSS variables in `:root` in `style.css`:
- `--navy` / `--navy-deep` — dark brown-black backgrounds
- `--gold` / `--gold-light` — terracotta accent colour
- `--cream` / `--warm-white` / `--alt-bg` — page backgrounds
- `--text` / `--muted` / `--border` — typography and dividers

The accessible version uses a separate high-contrast palette (blue accent `#004F9F`, black text on white).

## Fonts

Main version: **Playfair Display** (headings, italic) + **Inter** (body), loaded from Google Fonts.
Accessible version: **Inter** only.
