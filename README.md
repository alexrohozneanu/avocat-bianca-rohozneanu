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

1. Copiază șablonul: `cp docs/blog-template.html blog/<slug>.html`.
   Slug = titlul scurt, litere mici, fără diacritice, cuvinte separate cu
   cratimă (ex. `executarea-silita-a-pensiei-de-intretinere`).
2. Deschide fișierul și urmează instrucțiunile din comentariul de la început:
   înlocuiește TITLU, REZUMAT, SLUG, SLUG-EN, DATA-ISO, DATA-TEXT, șterge
   linia `noindex`, pune textul în `<div class="post-body">`.
3. Fă la fel pentru engleză în `en/blog/<slug-en>.html`, folosind
   `en/blog/child-support-enforcement.html` ca model pentru textele din meniu,
   CTA, disclaimer și footer.
4. Adaugă câte un card `<li class="post-card">` la **începutul** listei din
   `blog/index.html` și `en/blog/index.html` (modelul e la finalul șablonului).
5. Adaugă în `sitemap.xml`, înainte de `</urlset>`, două blocuri `<url>` (RO și EN),
   copiind blocurile existente pentru `child-support-enforcement.html` și
   schimbând adresele.

Verificare rapidă: `python3 -m http.server 8321`, deschide
`http://localhost:8321/blog/` și articolul nou, apasă butonul EN/RO din meniu.

## Publicare

Găzduit pe Netlify, conectat la acest repo — orice push pe `main` publică
automat. Formularul de contact folosește Netlify Forms; mesajele apar în
panoul Netlify → Forms (se poate configura notificare pe email).
