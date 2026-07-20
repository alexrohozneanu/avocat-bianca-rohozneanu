# Cabinet de Avocat Rohozneanu Bianca-Alexandra — site de prezentare

Site static bilingv (RO/EN): HTML + CSS, fără build, fără JavaScript.
Design cald (crem/nisip + auriu + antracit), găzduit pe Netlify.

## Structură

- `index.html` — pagina în română (implicită)
- `en/index.html` — pagina în engleză
- `multumim.html` / `en/thank-you.html` — paginile de confirmare după trimiterea formularului
- `css/style.css` — stilurile comune
- `fonts/` — fonturi servite local (Archivo, Playfair Display italic, Source Sans 3)
- `favicon.svg` — iconița site-ului

## Rulare locală

```bash
python3 -m http.server 8321
# apoi deschide http://localhost:8321/
```

## Cum actualizezi conținutul

Textul, datele de contact și cele opt domenii de practică sunt scrise direct
în `index.html` (română) și `en/index.html` (engleză). Caută secțiunea pe
care vrei s-o modifici (`<section id="despre">`, `id="domenii">`, `id="contact">`
etc.) și editează textul. Orice modificare în engleză trebuie făcută și în
pagina română, și invers.

Fotografie de profil: designul actual folosește un card cu repere în locul
unei poze. Dacă vrei să adaugi o fotografie, spune și o integrăm.

## Publicare

Găzduit pe Netlify, conectat la acest repo — orice push pe `main` publică
automat. Formularul de contact folosește Netlify Forms; mesajele apar în
panoul Netlify → Forms (se poate configura notificare pe email).
