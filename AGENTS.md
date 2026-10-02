# ameliapasser.com — Agent Guide

## Who you're working with

This site belongs to Amelia Passer, a painter and tarot artist in Boulder, CO.
**Amelia is not a programmer.** When working with her:

- Explain changes in plain language, by page and what it looks like ("the gold
  button at the top of the Events page"), never by file path, CSS class, or git
  jargon.
- Restate what you understood her request to be before making big changes, and
  after finishing, tell her exactly where on the site to look to see the result.
- Do only what she asked. If something adjacent seems broken or improvable,
  mention it — don't silently change it.
- If a request is ambiguous, ask one clear question rather than guessing.

Aaron Gabriel (GitHub: Unforced-Dev) built and maintains the site. For anything
involving payments, the domain, or anything that feels risky, pause and suggest
Amelia check with Aaron first.

## What this site is

A hand-written static site: plain HTML, one shared CSS file, a small shared JS
file. **No framework, no build step, no dependencies to install.** There is
nothing to compile and no test suite.

It is served by GitHub Pages from the `main` branch at https://ameliapasser.com.
**Anything merged to `main` is live on the public site within a minute or two.**
Therefore: always work on a branch and open a pull request rather than pushing
to `main` directly. In the PR description, explain the change in plain language
so Amelia can decide to merge it.

## Layout

- `index.html` — home page
- `pages/` — `gallery`, `tarot`, `readings`, `shop`, `events`, `about`
- `assets/styles.css` — the single shared stylesheet (design tokens in `:root`)
- `assets/script.js` — shared script (mobile nav toggle, reveal-on-scroll)
- `assets/images/` — artwork (`seven-basics/`, `minor-arcana/`, etc.)
- `CNAME`, `robots.txt`, `sitemap.xml` — infrastructure; see Rules below

## Design system

Dark celestial aesthetic: near-black background, gold accents
(`var(--gold)`, #d4af37), generous whitespace, serif display type.

- Fonts: Cormorant Garamond (display/headings), Inter (body), JetBrains Mono
  (small uppercase labels)
- Reusable patterns already in `styles.css` — use these before inventing new
  ones: `.section` + `.container` (and `.container--narrow`), `.eyebrow`,
  `.card`, `.ticket`, `.auction-card`, `.schedule`, `.event-meta`,
  `.btn--primary` / `.btn--ghost`, `.reveal` (scroll-in animation),
  `.divider` (the ✦ ornament)
- New CSS goes in `styles.css` next to related rules, using the existing
  custom properties. Match the existing tone — restrained, elegant, no
  off-palette colors.

## Rules

1. **The header/nav and footer are copy-pasted into every page** (no
   templating). If you change navigation or footer content, make the same
   change in `index.html` and every file in `pages/`.
2. **Never modify without explicit confirmation:** `CNAME` (the domain),
   Stripe payment links (`buy.stripe.com/...` URLs), and external service
   links (Givergy auction, etc.). Getting these wrong costs real money or
   takes the site down.
3. When adding or removing a page, update `sitemap.xml` and the nav/footer
   on all pages.
4. New images: keep them web-sized (long edge ≤ 2000px, JPEG, ideally under
   ~500 KB), put them under `assets/images/`, and always write meaningful
   `alt` text describing the artwork.
5. The site must work on phones — most visitors arrive from Instagram or QR
   codes. Existing breakpoints are at `max-width: 720px`; check your change
   makes sense at narrow widths.
6. Keep dates, times, and prices exactly as given — never round, reformat
   into a different timezone, or "improve" them.

## Verifying changes

There is no build step. To preview, open the HTML file directly in a browser,
or from the repo root run `python3 -m http.server` and visit
http://localhost:8000. Internal links between pages are relative
(`../assets/...` from inside `pages/`), so check them from the actual page
location, not just the repo root.
