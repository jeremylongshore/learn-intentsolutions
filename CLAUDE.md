# CLAUDE.md

Guidance for Claude Code sessions working in this repo.

## What this is

`learn.intentsolutions.io` — **Jeremy's personal study notes**. Public, but the audience is him later. Topics he's actively learning (currently: AWS) get a section with running notes plus the canonical reference links worth bookmarking.

Hugo static site. No DB, no auth, no API. Deploys to the Contabo VPS via the canonical VPS-as-the-home pattern (Tailscale OIDC + force-command SSH + Caddy).

**This is NOT a marketing site, NOT a routing hub for Jeremy's other properties, NOT a coaching offer page.** It is a personal learning destination. Frame all content as "Jeremy studying" not "Jeremy teaching."

## Stack + commands

```bash
hugo server -D              # local dev, http://localhost:1313
hugo --minify --gc          # production build → public/
```

Toolchain: Hugo extended (>= 0.161). No package manager — pure Hugo.

## Adding a new note

1. Drop a markdown file under `content/<topic>/<slug>.md` with frontmatter:
   ```yaml
   ---
   title: "Short noun-phrase title"
   date: 2026-MM-DD
   description: "One sentence — used as page-lede and in the section listing."
   weight: 20    # ordering within section; lower = earlier
   ---
   ```
2. Body uses standard Markdown. Code blocks, tables, blockquotes, headings (H2-H4) all styled in `assets/css/main.css`.
3. Commit + push. CI deploys in ~22s.

No `_index.md` change needed when adding a sub-page — the section template auto-lists it.

## Adding a new topic

1. `mkdir content/<topic>/`
2. Create `content/<topic>/_index.md` with `title`, `description`, and intro prose (canonical reference links go here; running notes append at the bottom).
3. Add to `hugo.toml` `[[menu.main]]`:
   ```toml
   [[menu.main]]
     name = "Topic"
     url = "/topic/"
     weight = 20    # menu order
   ```
4. Add notes as sub-pages per above.

## Architecture

- `hugo.toml` — site config, menu, params.
- `content/_index.md` — home page intro + auto-listed topic cards.
- `content/<topic>/_index.md` — topic landing (reference links + notes list).
- `content/<topic>/<slug>.md` — individual notes.
- `layouts/_default/baseof.html` — HTML skeleton, SEO meta.
- `layouts/index.html` — home page template (lists sections).
- `layouts/_default/list.html` — topic landing template.
- `layouts/_default/single.html` — individual note template (with prev/next nav).
- `layouts/partials/footer.html` — small footer.
- `assets/css/main.css` — reading-optimized dark theme, Charcoal Slate / Zinc tokens.
- `static/healthz` — VPS deploy smoke target.

## Deploy + infra

- Push to `main` → `.github/workflows/deploy.yml` → reusable workflow at `jeremylongshore/.github` → VPS deploy script `/usr/local/sbin/deploy-learn-intentsolutions`.
- VPS-side checkout: `/srv/learn-intentsolutions/`. Caddy serves directly from `/srv/learn-intentsolutions/public/`.
- Caddy block in `/etc/caddy/Caddyfile` — public, no basicauth.
- DNS: `learn.intentsolutions.io` A record → `167.86.106.29` (Porkbun, TTL 60s during soak, restore to 600s after 2026-06-07).

Operational rules:

1. **NEVER `systemctl restart caddy`** — only `caddy validate && systemctl reload caddy`. If reload times out at 90s (it can, on new-domain adds), fall back to `sudo caddy reload --config /etc/caddy/Caddyfile --force`. See memory `feedback_caddy_reload_systemd_timeout_workaround.md`.
2. **`gh secret set` requires direct `--body "$VALUE"`** for the 4 deploy secrets — never stdin (zsh glob-expansion bug silently corrupts).
3. **Reusable workflow SHA is pinned** at `709a07fbebb1d51806e171204e63f5332abcb0da`.

## Cross-references

- VPS onboarding procedure: `~/000-projects/intentsolutions-vps-runbook/docs/onboard-new-repo-deploy.md`
- Sibling Hugo deploy (partner-portals): `~/000-projects/partner-portals/`
- Brand color tokens source: `~/000-projects/intent-solutions-landing/astro-site/src/styles/global.css`
