# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Standing instruction — PRIMARY RULE

**Update this file immediately after every meaningful change, not at the end of the session.** Do not batch updates. Each time a feature is added, a decision is made, or a convention is established, update CLAUDE.md before moving on. Push the updated CLAUDE.md to GitHub alongside the relevant code changes. If asked whether CLAUDE.md is current, it should always be.

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

## CV page

`cv.html` mirrors the full LaTeX CV (`../sean_maroney_cv_latex/sean_cv/`). Sections in order: Research interests, Education, Publications, Employment, Service, Awards & Grants, Speaking Engagements, Languages, Creative Arts. When updating the LaTeX CV, recompile with `xelatex` and reflect any content changes in `cv.html` too.

## Conference presentation formatting

In `research.html`, conference presentations use a two-level hierarchy: the talk title is the primary text, and the venue/conference is wrapped in `<span class="conf-meta">` which renders as a smaller muted block below. The `.conf-meta` style is defined in `style.css`.

## CV PDF

The downloadable CV is compiled from LaTeX source at `../sean_maroney_cv_latex/sean_cv/main.tex` (relative to the website root). Must be compiled with **xelatex** (not pdflatex — uses fontspec). After compiling, copy `main.pdf` to `sean-maroney-cv.pdf` in the website root and push.

```bash
cd "../sean_maroney_cv_latex/sean_cv"
xelatex main.tex
cp main.pdf "../../Claude Code website v2.0/sean-maroney-cv.pdf"
```

## Favicon

`favicon.svg` — a φ (phi) character in terracotta (`#D4623E`) on navy (`#1A1714`), linked in the `<head>` of all 5 main pages. Not added to the accessible version.

## LaTeX CV — key conventions

- The LaTeX source is at `../sean_maroney_cv_latex/sean_cv/`. Files: `main.tex`, `title.tex`, `education.tex`, `publications.tex`, `employment.tex`, `service.tex`, `honors.tex`, `talks.tex`, `languages.tex`, `extra.tex`, `prometheus_cv.cls`.
- `\datedsubsection` — fuller entries (education, employment); has 3.5ex spacing before each item.
- `\datedsubsectionnarrow` — compact entries (talks, honors, service, creative arts); 0pt spacing before. Use this for denser sections.
- Speaking engagements: talk title is argument 3, venue is argument 4 (title is primary, venue subordinate).
- `prometheus_cv.cls` has been modified: entries with a non-blank 4th argument get `\vspace{0.7ex}` after the description to visually separate grouped entries.
- The PDF must be open in a viewer when recompiling — close it first or xelatex will fail with a file-lock error.

## Git setup

The local folder (`Claude Code website v2.0/`) is a git repo linked to `https://github.com/SeanThomist/Philosophy-Website.git`. Git user is configured locally (not globally). The `accessible/` folder and all assets are tracked and pushed alongside the HTML files.
