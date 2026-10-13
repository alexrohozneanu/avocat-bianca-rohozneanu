# Cabinet de Avocat Rohozneanu Bianca-Alexandra — site de prezentare

Site static bilingv (RO/EN): HTML + CSS, fără build, fără JavaScript.
Design cald (crem/nisip + auriu + antracit), găzduit pe Netlify.

## Structură

- `index.html` — pagina în română (implicită)
- `en/index.html` — pagina în engleză
- `multumim.html` / `en/thank-you.html` — paginile de confirmare după trimiterea formularului
- `blog/` și `en/blog/` — blogul: `index.html` (lista) + un fișier per articol
- `docs/blog-template.html` — șablon pentru articole noi
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

## Cum adaugi un articol pe blog

Blogul e static: fiecare articol e un fișier HTML, lista e întreținută manual.

1. **RO:** copiază șablonul, `cp docs/blog-template.html blog/<slug-ro>.html`,
   și urmează pașii din comentariul de la începutul lui (înlocuiești
   SLUG-RO, SLUG-EN, TITLU, REZUMAT, DATA-ISO, DATA-TEXT, ștergi linia `robots`
   și cele două comentarii, pui textul în `<div class="post-body">`).
   Slug = titlu scurt, litere mici, fără diacritice, cuvinte despărțite cu
   cratimă (ex. `executarea-silita-a-pensiei-de-intretinere`).
2. **EN:** nu porni de la șablon, copiază ultimul articol EN:
   `cp en/blog/child-support-enforcement.html en/blog/<slug-en>.html`, apoi
   schimbă `<title>`, meta description, cele două link-uri `hreflang`,
   link-ul RO din meniu, `<h1>`, data (ex. `13 October 2026`) și textul.
3. **Liste:** adaugă câte un card `<li class="post-card">` la **începutul**
   listei din `blog/index.html` (card RO) și `en/blog/index.html` (card EN).
   Modelele sunt în comentariul de la finalul șablonului.
4. **Sitemap:** în `sitemap.xml`, înainte de `</urlset>`, copiază cele două
   blocuri `<url>` ale ultimului articol (RO și EN) și schimbă adresele.
5. **Verificare înainte de push:**

   ```bash
   grep -n 'noindex\|SLUG\|TITLU\|REZUMAT\|DATA-' blog/<slug-ro>.html en/blog/<slug-en>.html
   ```

   trebuie să nu afișeze nimic. Apoi `python3 -m http.server 8321`, deschide
   `http://localhost:8321/blog/` și cele două articole și apasă butonul EN/RO din meniu.

## Publicare

Găzduit pe Netlify, conectat la acest repo — orice push pe `main` publică
automat. Formularul de contact folosește Netlify Forms; mesajele apar în
panoul Netlify → Forms (se poate configura notificare pe email).
