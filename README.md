# portfolio-cv

Adrian Dragota's personal portfolio/CV site, meant to run on the root domain
`adriandragota.com`.

Static, no build step, no framework — plain HTML/CSS/JS, served by a single
nginx container behind the sibling `fanvote` stack's Caddy reverse proxy.

## Structure

```
index.html                          # the whole site, anchored sections (#about, #experience, ...)
assets/style.css                     # all styling, CSS variables for the palette
assets/script.js                     # mobile nav toggle + current year in the footer
assets/files/Adrian-Dragota-CV.pdf   # downloadable CV
docker-compose.prod.yml              # production: one nginx:alpine container
```

## Running locally

Any static server works, e.g.:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploy

No backend, no database, no auth — one static-file container.

```bash
docker compose -f docker-compose.prod.yml up -d --build
```

This requires the `shared-infra` Docker network to already exist (created by
the sibling `fanvote` project's `docker-compose.prod.yml` — start that stack
first). Caddy on that same machine reverse-proxies `PORTFOLIO_DOMAIN` (and
`www.`) to this container by name (`portfolio-cv:80`) — see `deploy/Caddyfile`
and `.env.prod.example` in the `fanvote` repo.

## Still to do

- The project cards (`.project-visual--*`) are CSS mockups for now, not real
  screenshots — swap them in once `shop.adriandragota.com` and
  `clinica.adriandragota.com` are actually live.
- The phone number was deliberately left off the public page (email + LinkedIn
  only) — add it back if that's not what you want.
