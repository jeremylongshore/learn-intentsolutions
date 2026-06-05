# learn.intentsolutions.io

Public learning hub for Intent Solutions. Routes arriving visitors to the right resource across Jeremy Longshore's seven web properties: blog, plugins, open source, partner work, coaching, portfolio.

- **Live**: https://learn.intentsolutions.io
- **Stack**: Hugo (static), Caddy on Contabo VPS, GitHub Actions deploy via Tailscale OIDC
- **License**: MIT

## Local dev

```bash
hugo server -D
# open http://localhost:1313
```

## Deploy

Push to `main` triggers `.github/workflows/deploy.yml`. The reusable workflow at
`jeremylongshore/.github/.github/workflows/vps-deploy.yml` handles Tailscale OIDC →
SSH → force-command deploy script on the VPS. ~22s end to end.

Manual verify after push:

```bash
curl -fsS https://learn.intentsolutions.io/healthz | jq
# {"ok":true,"service":"learn.intentsolutions.io"}
```

## Reference

- VPS onboarding procedure: `intentsolutions-vps-runbook/docs/onboard-new-repo-deploy.md`
- Sibling property (partner-portals): https://github.com/jeremylongshore/partner-portals
