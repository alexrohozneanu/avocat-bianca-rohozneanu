# Blog section — design spec

**Date:** 2026-10-13
**Status:** approved in conversation, pending written review

## Intent

Bianca (the client) wants to publish legal articles on the site, in Romanian
and English. Alex publishes on her behalf: she sends the text, he (or Claude)
puts it on the site via git. Expected rhythm is roughly one article a month.
One article exists today (`~/Downloads/articol.rtf`, Romanian only).

Success looks like: a `/blog/` section that matches the existing design,
one published article in both languages, and a README recipe so Alex can add
the next article without help.

## Constraints (from the existing site)

- Static HTML + one shared CSS file. **No build step, no JavaScript, no
  dependencies.** This is the deciding constraint; it is why a static site
  generator or a CMS was rejected.
- Bilingual: every RO page has an EN twin, cross-linked with `hreflang` in
  `<head>` and in `sitemap.xml`, plus a RO/EN switch in the nav.
- Fonts served locally; palette and components from `css/style.css`.
- Hosted on Netlify; `main` is production, `dev` is a branch deploy.

## Decisions made during brainstorming

| Question | Decision |
|---|---|
| Who publishes? | Alex, via git. No CMS. |
| Languages | RO and EN, every article translated. |
| Existing content | One RO article. Claude translates it to EN as a draft for Bianca to review. |
| Build approach | Plain HTML per article (option A). Markdown+Eleventy (B) and a local generator script (C) rejected as over-engineering at ~1 article/month. |
| Homepage section | None for now. Add a "latest articles" block once there are 3+ articles. |
| Categories, pagination, cover images | None. Revisit at 15–20 articles. |

## URL structure

| Page | RO | EN |
|---|---|---|
| Listing | `/blog/index.html` → `/blog/` | `/en/blog/index.html` → `/en/blog/` |
| Article | `/blog/<slug>.html` | `/en/blog/<slug-en>.html` |
| First article | `/blog/executarea-silita-a-pensiei-de-intretinere.html` | `/en/blog/child-support-enforcement.html` |

Articles keep the `.html` extension to match `termeni.html` etc. Slugs are
lowercase ASCII, words separated by hyphens, diacritics stripped. The EN slug
is a translation, not a transliteration.

All blog pages use **absolute** paths for shared assets (`/css/style.css`,
`/favicon.svg`) so the same markup works from `/blog/` and `/en/blog/`.

## Pages

### Listing page (`/blog/`, `/en/blog/`)

- Same header/footer as the legal pages, with the nav's "Blog" item marked
  current and the RO/EN switch pointing at the other listing.
- Hero in the `section-head` style: eyebrow "Blog", H1 "Articole" / "Articles",
  one-line intro ("Explicații practice despre probleme juridice frecvente." /
  equivalent).
- A list (`<ul class="post-list">`) of cards, newest first. Each card:
  `<time>` with the publication date (`<time datetime="2026-10-13">13 octombrie 2026</time>`),
  the title as a link, a 1–2 sentence summary.
- New articles are added by hand at the top of the list.

### Article page

- Reuses the `.legal` single-column layout (48rem) under a new class
  `.post` so blog-specific styles don't leak into legal pages.
- `<article class="post wrap">` containing: eyebrow "Blog", H1 title,
  `<p class="post-meta">` with `<time>` and author "Av. Bianca Rohozneanu",
  then the body: `<p>`, `<h2>`, `<ul>/<li>`, `<strong>`, `<a>`. These are
  the only elements the first article needs; the template documents them.
- After the body, two blocks:
  1. **Contact call-out** (`.post-cta`): short sentence + `btn btn-primary`
     linking to `/#contact` (RO) or `/en/#contact` (EN).
  2. **Disclaimer** (`.post-disclaimer`): one sentence stating the article
     is informational and not legal advice, consistent with `termeni.html`
     §2 and `en/terms.html`.
- "← Înapoi la articole" / "← Back to articles" link at the bottom.
- `<head>`: title "<Article title> — Avocat Bianca Rohozneanu", meta
  description = the listing summary, `hreflang` ro/en pair, canonical not
  needed (site already omits it), favicon, stylesheet.

### Template (`docs/blog-template.html`)

A copy-ready article page with placeholder tokens in CAPS
(`TITLU`, `SLUG`, `DATA-ISO`, `DATA-TEXT`, `REZUMAT`, body), plus an HTML
comment at the top listing the steps. Lives in `docs/` so Netlify serves it
but nothing links to it; it carries `<meta name="robots" content="noindex">`.
One template serves both languages: the comment explains which strings to
swap for EN.

## Site integration

- **Nav** on every page (home, legal, thank-you, both languages): add
  "Blog" before "Contact", linking to `/blog/` or `/en/blog/`. On the
  homepage the other items are `#anchors`; "Blog" is a normal link.
- **Footer** on every page: add "Blog" to `.foot-links`.
- **Sitemap**: add `/blog/`, `/en/blog/`, and the article pair, each with
  the three `xhtml:link` alternates (ro, en, x-default → ro). Keep
  `lastmod` out, consistent with existing entries.
- **robots.txt**: unchanged.
- **README**: new section "Cum adaugi un articol" with the 5 steps:
  copy template → fill RO → fill EN → add card to both listings →
  add 2 `<url>` blocks to sitemap. Mention the slug rules and the date
  formats.

## CSS additions (`css/style.css`)

Appended under a `/* ---- Blog ---- */` comment, before the media queries:

- `.post-list`, `.post-card` (border, radius, hover like `.card`), `.post-card time`
  (gold, small caps spacing like `.eyebrow`), `.post-card h2`, `.post-card p`.
- `.post` inherits spacing from `.legal` by sharing rules (`.legal, .post {…}`)
  rather than duplicating; add `.post h1` size, `.post-meta`, `.post p`
  line-height 1.7 and font-size 1.08rem for readability, `.post h2`, `.post ul`.
- `.post-cta` (sand-2 background, radius, padding, button inside),
  `.post-disclaimer` (small, ink-soft, top border).
- `.nav-links a[aria-current="page"]` gold underline so "Blog" reads as current
  on blog pages.

No new tokens, no new fonts.

## First article content

- RO: text from `articol.rtf` verbatim, structured as H1 + intro paragraphs,
  three H2 sections ("Cum se poate recupera…", "Ce documente sunt necesare?",
  "Ce se întâmplă dacă nu plătește…") with their lists/paragraphs.
- EN: Claude's translation, titled "Enforcing child support: what to do when
  the other parent doesn't pay". Flagged in the commit message and in the
  final message to Alex as a draft for Bianca's review.
- Date: the day of publication (set when the page is built).

## Error handling

Static site: the only failure modes are broken links and missing files.
Mitigation is the verification list below plus Netlify's default 404.

## Verification

1. `python3 -m http.server 8321` and `curl` every new URL (2 listings, 2
   articles, template) → 200.
2. `tidy -q -e` (or `xmllint --html`) on each new file → no errors.
3. `grep` that every page's `hreflang` pair points at a file that exists and
   that the pair is reciprocal.
4. `xmllint --noout sitemap.xml` → well-formed; `grep -c '<url>'` = 10.
5. Visual check at desktop and 390px width: nav wraps, cards stack, article
   column reads comfortably.
6. Every page in the site (8 existing + 4 new, RO+EN) has the "Blog" nav and
   footer link: `grep -L 'href="/blog/"\|href="/en/blog/"' *.html en/*.html blog/*.html en/blog/*.html`
   → only `googlecaf98bf648c2b375.html` (the Search Console file, never edited).

## Out of scope

RSS feed, search, comments, tags, author pages, related-articles block,
homepage teaser, EN-only or RO-only articles, images inside articles
(add `<figure>` styling when the first article with an image arrives).
