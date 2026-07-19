# Design: Site de prezentare — Avocat Bianca Rohozneanu

**Data:** 19 iulie 2026
**Status:** Aprobat de Alex

## Scop

Site simplu de promovare pentru Bianca Rohozneanu, avocat în Cluj-Napoca.
Scopul: prezență profesională online, prezentarea domeniilor de practică și
un mod ușor pentru potențiali clienți de a o contacta.

## Conținut și structură

Site de tip "one-page" (o singură pagină cu secțiuni), navigare cu derulare
la secțiune, plus versiune în engleză ca pagină separată.

Secțiuni, în ordine:

1. **Hero** — „Avocat Bianca Rohozneanu", subtitlu „Cabinet de avocatură ·
   Cluj-Napoca", buton principal „Contactează-mă" care derulează la secțiunea
   de contact.
2. **Despre** — biografie scurtă. *Text provizoriu până primim datele reale.*
3. **Domenii de practică** — trei carduri, fiecare cu titlu, pictogramă
   discretă și descriere de 2-3 fraze:
   - Drept civil
   - Drept comercial
   - Dreptul familiei
4. **Contact** — formular (nume, email, mesaj) prin Netlify Forms; alături,
   date de contact: telefon, email, adresă. *Toate provizorii deocamdată.*

**Footer** — nume, an, mențiune barou (provizoriu).

## Bilingv (RO / EN)

- Româna e limba implicită: `index.html`.
- Engleza: `en/index.html`, aceeași structură, texte traduse.
- Comutator RO/EN în colțul din dreapta sus al navigării, pe ambele pagini.
- Două pagini statice separate — fără JavaScript de traducere; simplu și
  corect pentru SEO (`hreflang` în `<head>`).

## Stil vizual

Direcție: **clasic și elegant** — stilul tradițional al cabinetelor de
avocatură, transmite încredere.

- **Culori:** bleumarin închis (fundal secțiuni cheie), crem/alb (fundal
  principal), accente aurii (butoane, linii decorative).
- **Tipografie:** serife pentru titluri (Playfair Display), sans-serif
  pentru corp (Source Sans 3 sau similar). Fonturile se servesc local
  (fișiere în repo), nu de la Google — mai rapid și fără implicații GDPR.
- **Responsive:** mobil-first; cardurile de domenii se așază vertical pe
  telefon.

## Tehnologie

- HTML + CSS pur, fără framework, fără proces de build.
- Un singur fișier CSS partajat de ambele versiuni lingvistice.
- JavaScript minim sau deloc (eventual doar pentru meniul mobil).

## Structura fișierelor

```
avocat-bianca-rohozneanu/
├── index.html          # versiunea română
├── en/index.html       # versiunea engleză
├── css/style.css
├── fonts/              # fonturi locale (woff2)
├── img/                # poză profil (provizoriu un placeholder)
└── docs/superpowers/specs/   # acest document
```

## Publicare

1. Repo public pe GitHub, contul `alexrohozneanu`.
2. Netlify (plan gratuit) conectat la repo — deploy automat la fiecare push,
   HTTPS inclus, Netlify Forms pentru formularul de contact.
3. Ulterior: domeniu propriu (ex. `rohozneanu.ro` sau `avocatrohozneanu.ro`,
   ~50-60 lei/an), configurat prin DNS către Netlify.

## Conținut provizoriu (de înlocuit)

Marcat clar în cod cu comentarii `<!-- PROVIZORIU -->`:

- Biografia (experiență, studii, barou)
- Telefon, email, adresa cabinetului
- Poza de profil
- Descrierile detaliate ale domeniilor de practică (versiune generică
  inițial, de rafinat cu Bianca)

## Criterii de succes

- Site-ul se încarcă rapid (< 1s) și arată corect pe telefon și desktop.
- Formularul de contact trimite mesaje funcțional prin Netlify Forms.
- Ambele versiuni lingvistice sunt complete și legate corect între ele.
- Textele provizorii pot fi înlocuite ușor, fără cunoștințe tehnice avansate.

## În afara scopului (deocamdată)

- Blog / articole
- Programări online
- CMS sau panou de administrare
- Analytics (se poate adăuga ulterior, ex. Plausible/umami, fără cookies)
