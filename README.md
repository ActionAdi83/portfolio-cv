# portfolio-cv

Site personal de portofoliu/CV pentru Adrian Dragota, gândit să ruleze pe
domeniul rădăcină `adriandragota.com`.

Static, fără build step, fără framework — HTML/CSS/JS simplu, servit direct
de un reverse proxy (Caddy `file_server`) sau de orice server static.

## Structură

```
index.html            # singura pagina, cu sectiuni ancorate (#despre, #experienta, ...)
assets/style.css       # tot stilul, variabile CSS pentru paleta de culori
assets/script.js       # meniu mobil + anul curent in footer
assets/files/Adrian-Dragota-CV.pdf   # CV descarcabil
```

## Rulare locală

Orice server static merge, de exemplu:

```bash
npx serve .
# sau
python3 -m http.server 8000
```

## Deploy

Nu are backend și nu are nevoie de Docker/Mongo/Keycloak — se copiază pur și
simplu conținutul pe server și se adaugă un vhost Caddy:

```caddyfile
adriandragota.com, www.adriandragota.com {
    root * /srv/portfolio-cv
    file_server
}
```

## De actualizat mai târziu

- Cardurile de proiecte (`.project-visual--*`) sunt momentan mockup-uri CSS
  (nu capturi reale) — de înlocuit cu screenshot-uri reale odată ce
  `shop.adriandragota.com` și `clinica.adriandragota.com` sunt live.
- Numărul de telefon a fost lăsat intenționat în afara paginii publice
  (doar email + LinkedIn) — de adăugat dacă se dorește altfel.
