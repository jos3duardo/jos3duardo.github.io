# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static personal portfolio/landing page for José Eduardo Lopes de Souza (jos3duardo.com.br), hosted via GitHub Pages. Single-page site, no JavaScript of its own: the name in the hero is "printed" layer by layer (CSS clip-path with steps(), stripes as FDM layer lines). Analytics via Tianji.

## Architecture

- **`index.html`** — The entire site is a single HTML file. No build step, no static site generator.
- **`assets/css/style.css`** — The only stylesheet. Color tokens on `:root`, dark mode via `prefers-color-scheme`. Fonts (Bricolage Grotesque, Schibsted Grotesk) come from Google Fonts.
- Sections use a two-column grid (section name rail + content); the experience timeline is an `<ol reversed>`.

## Deployment

- **GitHub Pages** serves the site directly from the `master` branch — any push to `master` deploys.
- **Production today** is the nginx container on oci-pessoal serving the clone at `~/projetos/jos3duardo/jos3duardo.github.io`: deploy = push to `master`, then `git pull` there (and `docker compose up -d` when `docker-compose.yml`/`nginx.conf` change). `nginx.conf` returns 404 for dotfiles (`.git`, `.claude`) and repo-internal files — new internal files at the root must be added there.
- **Docker/Traefik** (`docker-compose.yml`) — Alternative self-hosted deployment using nginx + Traefik reverse proxy with Let's Encrypt TLS on domain `jos3duardo.com.br`. Requires an external Docker network named `proxy`.
- **`tests.traefik.yml`** — Standalone Traefik test config with a whoami service on `teste.jos3duardo.com.br`.

## Local Development

Open `index.html` directly in a browser, or `python3 -m http.server 8090`. For Docker-based serving:

```bash
docker compose up -d
```

## Analytics

Tianji analytics is embedded via the tracker script in `index.html`. Tianji is self-hosted on oci-pessoal (`~/projetos/docker-compose/tianji`) at `tianji.jos3duardo.com.br`.
