# CLAUDE.md

Guidance for Claude Code sessions working in this repo.

## What this is

`learn.intentsolutions.io` — public learning hub that triages arriving visitors to the right Intent Solutions property (blog / plugins / open source / partner work / coaching / portfolio).

Hugo static site. No DB, no auth, no API. Deploys to the Contabo VPS via the canonical VPS-as-the-home pattern (Tailscale OIDC + force-command SSH + Caddy).

## Stack + commands

```bash
hugo server -D              # local dev, http://localhost:1313
hugo --minify --gc          # production build → public/
```

Toolchain: Hugo extended (>= 0.161). No package manager — pure Hugo.

## Architecture

- `hugo.toml` — site config, params.
- `content/_index.md` — minimal; the landing page is composed entirely by layouts.
- `layouts/_default/baseof.html` — HTML skeleton, SEO meta, schema JSON-LD.
- `layouts/index.html` — landing page composition (defines `title`, `schema`, `main` blocks).
- `layouts/partials/{hero,role-triage,property-cards,featured,faq,footer}.html` — sections.
- `assets/css/main.css` — single CSS file processed by Hugo Pipes (minified + fingerprinted).
- `static/healthz` — VPS deploy smoke target. Must return `{"ok":true,"service":"learn.intentsolutions.io"}`.

## Design system

Charcoal Slate / Zinc base (consistent with `intentsolutions.io` global.css tokens) + brutalist CTA accents (stark borders, no shadow blur, hover-shift transform). Inter font via rsms.me CDN. Mobile-first responsive.

Tokens in `assets/css/main.css` :root — change once, propagate everywhere.

## Adding content

`content/guides/<slug>.md` will render as `learn.intentsolutions.io/guides/<slug>/` once a section layout exists. v1 ships with no guides — the hub is landing-page only. When the first guide ships, add `layouts/guides/single.html` and a list partial.

## Deploy + infra

- Push to `main` → `.github/workflows/deploy.yml` → reusable workflow at `jeremylongshore/.github` → VPS deploy script `/usr/local/sbin/deploy-learn-intentsolutions`.
- VPS-side checkout: `/srv/learn-intentsolutions/`. Caddy serves directly from `/srv/learn-intentsolutions/public/`.
- Caddy block in `/etc/caddy/Caddyfile` — public, no basicauth, no rewrite tricks.
- DNS: `learn.intentsolutions.io` A record → `167.86.106.29` (Porkbun).

Operational rules:

1. **NEVER `systemctl restart caddy`** — only `caddy validate && systemctl reload caddy`. Restart kills the other 24 prod containers' TLS state.
2. **`gh secret set` requires direct `--body "$VALUE"`** for the 4 deploy secrets — never stdin (zsh glob-expansion bug silently corrupts).
3. **Reusable workflow SHA is pinned** at `709a07fbebb1d51806e171204e63f5332abcb0da`. Bump only after reviewing diff against `jeremylongshore/.github` main.

## Cross-references

- VPS onboarding procedure: `~/000-projects/intentsolutions-vps-runbook/docs/onboard-new-repo-deploy.md`
- First-time-onboarding gotchas: `~/000-projects/intentsolutions-vps-runbook/plans/2026-05-01-vps-as-the-home/08-aar-priority-5-followup-lilly-75-holy-onboarding-2026-05-03.md`
- Sibling Hugo deploy (partner-portals): `~/000-projects/partner-portals/`
- Brand color tokens source: `~/000-projects/intent-solutions-landing/astro-site/src/styles/global.css`
