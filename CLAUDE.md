# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Standing instruction

Update this file during every session whenever a meaningful change is made — new features, structural decisions, deployment steps, or anything a future session would need to know. Push the updated CLAUDE.md to GitHub alongside the relevant code changes.

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

## Mobile responsiveness (main version)

Added April 2026. All mobile styles live in a single `@media (max-width: 768px)` block at the bottom of `style.css`. Key behaviours:
- Nav collapses to a hamburger button; toggled by `nav.js`
- Hero stacks to single column with photo above text
- All multi-column grids (research interests, public philosophy, CV, contact) collapse to one column

The accessible version already handled mobile via `flex-wrap` — no hamburger needed there.

## Conference presentation formatting

In `research.html`, conference presentations use a two-level hierarchy: the talk title is the primary text, and the venue/conference is wrapped in `<span class="conf-meta">` which renders as a smaller muted block below. The `.conf-meta` style is defined in `style.css`.

## Git setup

The local folder (`Claude Code website v2.0/`) is a git repo linked to `https://github.com/SeanThomist/Philosophy-Website.git`. Git user is configured locally (not globally). The `accessible/` folder and all assets are tracked and pushed alongside the HTML files.
