# Avocat Bianca Rohozneanu — site de prezentare

Site static bilingv (RO/EN): HTML + CSS, fără build, fără JavaScript.

## Structură

- `index.html` — pagina în română (implicită)
- `en/index.html` — pagina în engleză
- `css/style.css` — stilurile comune
- `fonts/` — fonturi servite local (Playfair Display, Source Sans 3)
- `img/` — imagini

## Rulare locală

```bash
python3 -m http.server 8321
# apoi deschide http://localhost:8321/
```

## Cum actualizezi conținutul

Tot textul provizoriu este marcat în HTML cu comentariul `<!-- PROVIZORIU -->`
pe rândul de deasupra. Caută `PROVIZORIU` în `index.html` și `en/index.html`
și înlocuiește textul de sub fiecare marcaj (biografie, telefon, email,
adresă, poză). După înlocuire, șterge comentariul.

Poza de profil: înlocuiește `img/portret-placeholder.svg` cu o fotografie
reală (ex. `img/portret.jpg`, ~440×520px) și actualizează atributul `src`
în ambele pagini.

## Publicare

Găzduit pe Netlify, conectat la acest repo — orice push pe `main` publică
automat. Formularul de contact folosește Netlify Forms; mesajele apar în
panoul Netlify → Forms (se poate configura notificare pe email).
