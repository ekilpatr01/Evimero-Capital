---
name: seo-check
description: Audit and improve the SEO/social-preview metadata of the Evimero Capital site (index.html) — meta description, Open Graph, Twitter cards, canonical, title, favicons. Use when the user asks about SEO, search ranking, link previews, sharing on social/LinkedIn, or before a public launch.
---

# SEO & social-preview audit for index.html

Single-page site, so all metadata lives in the one `<head>` of `index.html`. Audit against this checklist and add what's missing.

## Current state (baseline — likely still true)

- ✅ `<title>`, `charset`, `viewport`, `theme-color`, favicons (base64) present.
- ❌ **No `<meta name="description">`** — search snippets are auto-generated / poor.
- ❌ **No Open Graph tags** — LinkedIn/Facebook/Slack link previews show nothing.
- ❌ **No Twitter Card tags.**
- ❌ No `<link rel="canonical">`, no structured data.

Re-verify with a quick grep before acting, since the file may have changed.

## What to add (in `<head>`)

```html
<meta name="description" content="Evimero Capital is a boutique private investment office — principal investment, investment advisory, and M&A, capital raising & strategic advisory. Institutional pedigree, global experience.">
<link rel="canonical" href="https://evimerocapital.com.au/">

<!-- Open Graph -->
<meta property="og:type" content="website">
<meta property="og:site_name" content="Evimero Capital">
<meta property="og:title" content="Evimero Capital — Private Investment Office">
<meta property="og:description" content="Boutique private investment office: principal investment, advisory, and M&A / capital raising.">
<meta property="og:url" content="https://evimerocapital.com.au/">
<meta property="og:image" content="https://evimerocapital.com.au/og-image.png">

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Evimero Capital — Private Investment Office">
<meta name="twitter:description" content="Boutique private investment office: principal investment, advisory, and M&A / capital raising.">
<meta name="twitter:image" content="https://evimerocapital.com.au/og-image.png">
```

## Notes & follow-ups

- Keep copy in the formal brand voice (see `brand-style` / `edit-content`). Australian English.
- `og:image` needs a real 1200×630 image at that URL. Flag to the user that one must be created and committed (or embed as an absolute URL) — a broken image URL is worse than none. Until it exists, either omit the image tags or point them at a real hosted asset.
- Consider `JSON-LD` structured data (`Organization` / `FinancialService`) with name, url, logo, email `info@evimerocapital.com.au`, and address for richer search results.
- Add a `robots` meta / `sitemap.xml` only once the site is meant to be indexed.
- After changes, run `preview` and check the `<head>` renders without breaking the page.
