# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static personal portfolio/landing page for José Eduardo Lopes de Souza (jos3duardo.com.br), hosted via GitHub Pages. Single-page site with a particles.js animated background, social links, and analytics tracking via Tianji.

## Architecture

- **`index.html`** — The entire site is a single HTML file. No build step, no static site generator.
- **`assets/`** — CSS (`main.css`, `timeline.css`), JS (`main.js`, `particles.min.js`, `sweet-scroll.min.js`), and fonts (Font Awesome, Devicon).
- **`main.js`** — Initializes SweetScroll and particles.js with configuration (polygon particles, white on dark background).
- **`main.css`** — Large hand-written stylesheet (not generated). Timeline styles are separate in `timeline.css`.

## Deployment

- **GitHub Pages** serves the site directly from the `master` branch — any push to `master` deploys.
- **Docker/Traefik** (`docker-compose.yml`) — Alternative self-hosted deployment using nginx + Traefik reverse proxy with Let's Encrypt TLS on domain `jos3duardo.com.br`. Requires an external Docker network named `proxy`.
- **`tests.traefik.yml`** — Standalone Traefik test config with a whoami service on `teste.jos3duardo.com.br`.

## Local Development

Open `index.html` directly in a browser — no server or build required. For Docker-based serving:

```bash
docker compose up -d
```

## Analytics

Tianji analytics is embedded via a tracker script and a tracking pixel in `index.html`, pointing to `tianji.jos3duardo.com.br`.
