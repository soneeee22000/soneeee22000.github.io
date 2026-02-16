# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site — personal portfolio for Pyae Sone (Seon). Single-page design with all content configured in `hugo.toml` (no separate `content/` directory). Deployed to GitHub Pages at `https://soneeee22000.github.io/`.

## Build & Development Commands

```bash
# Local development server (with drafts)
hugo server -D

# Production build (matches CI)
hugo --gc --minify

# Initialize/update theme submodule after clone
git submodule update --init --recursive
```

Hugo version used in CI: **0.115.1 extended**. Install matching version locally.

## Architecture

- **Theme**: `hugoProfileReforge` — custom fork of [hugo-profile](https://github.com/gurusabarish/hugo-profile), managed as a git submodule at `themes/hugoProfileReforge/`
- **All site content** lives in `hugo.toml` params (hero, about, experience, education, projects, achievements, contact) — not in markdown files
- **Static assets**: `static/images/` for profile photos, project screenshots (`projects/`), and certificates (`certs/`)
- **Theme customization**: The main fork change is in `themes/hugoProfileReforge/layouts/partials/sections/about.html` — skills rendered as image logos instead of text lists, styled via `themes/hugoProfileReforge/static/css/about.css`

## Theme Structure (key files)

- `layouts/partials/sections/` — each portfolio section (hero, about, experience, education, projects, achievements, contact)
- `static/css/` — per-section CSS files + `theme.css` for dark/light mode
- `static/js/` — search, contact form, scroll progress bar
- Self-hosted Bootstrap 5 and FontAwesome 5 (no CDN)

## Deployment

GitHub Actions workflow (`.github/workflows/hugo.yaml`) auto-deploys on push to `main`:

1. Checks out with recursive submodules
2. Builds with `hugo --gc --minify`
3. Deploys to GitHub Pages

## Content Updates

To add/edit portfolio content, modify the relevant `[params.X]` sections in `hugo.toml`. Sections in order: hero, about, experience, education, projects, achievements, contact.
