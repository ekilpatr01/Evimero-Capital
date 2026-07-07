---
name: edit-content
description: Guide to safely editing the Evimero Capital site, which lives entirely in one large single-file index.html (all CSS and JS inline). Use when adding, removing, or rewriting page copy or sections, so you know where content lives, the brand voice, and which parts of the file must not be disturbed.
---

# Editing index.html (single-file site)

The whole site is **one file**, `index.html` (~540 KB, ~935 lines). Everything is inline: one `<style>` block, one `<script>` block, and favicons/images embedded as base64 data URIs. There is no framework, no build, no partials. Edit with targeted `Edit` calls — never rewrite the whole file, and never reformat unrelated regions (git history shows edits done as full-file re-uploads; keep diffs small and reviewable instead).

## Page structure (in document order)

| Section | Selector | Content |
|---------|----------|---------|
| Nav | `nav` / `.nav-*` | Logo "Evimero Capital", links, CTA button |
| Hero | `<section id="hero">` | `.hero-headline`, `.hero-sub`, `.hero-actions` on navy |
| About | `<section id="about">` | "Global experience…" title, `.body-text`, `.about-stats` band |
| Services | `<section id="services">` | 3 `.service-card`s: Principal Investment; Investment Advisory; M&A, Capital Raising & Strategic Advisory |
| Stats | within about/services | `.stat-card`s: Year Founded, Market Reach, Asset Classes, Institutional Pedigree |
| Contact | `<section id="contact">` | Office + Email details, contact form, footer |

## Where the heavy/fragile bytes are

- **Base64 blobs** (favicons, any embedded imagery) are long single-line `data:image/...;base64,...` strings. Do not edit inside them, and don't let a search-and-replace span them.
- **`<style>` block** — the whole design system. To restyle, read the `brand-style` skill first and edit tokens/classes there.
- **`<script>` block** (near the end) — handles: sticky nav, IntersectionObserver scroll-reveal, and the contact-form submit. Small; don't break it.

## Brand voice for copy

Formal, understated, institutional. Think private bank / family office, not startup. Prefer "global experience," "institutional pedigree," "principal investment." No exclamation marks, no emoji, no hype. Australian English spelling.

## Known content caveats

- ⚠️ The **contact form is a stub** — its submit handler just waits 1.2s and shows a fake success message; nothing is sent. If asked to "make the form work," see the `seo-check`/deploy notes and wire it to a real endpoint (e.g. Formspree, or `mailto:` fallback to `info@evimerocapital.com.au`). Don't imply it works when it doesn't.
- The stat numbers (`.stat-num`) are marketing figures — confirm values with the user before changing them.

## After any edit

Run the `preview` skill to serve and screenshot the result. Verify reveal animations still fire and both desktop + mobile render. Keep the commit message specific about what copy/section changed.
