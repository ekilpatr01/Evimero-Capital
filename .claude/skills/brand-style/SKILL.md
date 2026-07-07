---
name: brand-style
description: The Evimero Capital brand and design system — colors, fonts, spacing tokens, and component styles. Read this BEFORE adding or editing any visual element in index.html (buttons, sections, cards, colors, type) so changes stay on-brand and consistent. Use when the user asks to restyle, add a section, change colors, or adjust the look of the site.
---

# Evimero Capital — brand & design system

Evimero Capital is a boutique private investment office. The visual language is **institutional, restrained, and premium**: deep navy, warm cream/parchment backgrounds, and a muted antique-gold accent. Serif display type over clean sans body. Avoid anything loud, bright, or "startup-y."

## Design tokens (defined as CSS custom properties in `:root`)

Always use the variable, never a raw hex, so the palette stays centralized.

| Token | Value | Use |
|-------|-------|-----|
| `--cream` | `#F5F1EA` | primary light background |
| `--cream-dk` | `#EDE8DF` | alternating section background |
| `--parchment` | `#DED8CB` | subtle panels / borders |
| `--charcoal` | `#1C1A16` | primary body text on light |
| `--navy` | `#0D1E35` | dark sections (hero, contact) |
| `--navy-dk` | `#081526` | deepest navy, gradients |
| `--stone` | `#7A7468` | muted/secondary text |
| `--gold` | `#B8943F` | primary accent, rules, icons |
| `--gold-lt` | `#D4AE5A` | hover/highlight gold |
| `--gold-dk` | `#8A6E2A` | pressed/darker gold |
| `--rule` | `rgba(184,148,63,.2)` | hairline dividers |

Note: the visible CTA button uses `#e8c370` for its background/hover — keep that consistent if you touch `.btn-submit` / `.nav-cta`.

## Type

- `--serif: 'Playfair Display', Georgia, serif;` — headings, hero, section titles.
- `--sans: 'Lato', sans-serif;` — body, labels, buttons, nav.
- Loaded from Google Fonts (weights: Playfair 400/500/700 + italics; Lato 300/400/700). Keep the `<link rel="preconnect">` before the stylesheet link.

## Motion & spacing

- `--ease: cubic-bezier(.22,.68,0,1.2)` — the house easing (slight overshoot). Use it for transitions.
- `--px: clamp(20px, 5vw, 60px)` — standard horizontal page padding.
- `--nav-h` — sticky nav height (68px desktop / 60px mobile).
- Scroll-reveal: add class `reveal` (starts hidden, animates in on scroll) plus optional `reveal-delay-1..4` for stagger. An IntersectionObserver in the `<script>` toggles these — new content that should animate in must use these classes.

## Component conventions

- **Section titles**: `<h2 class="section-title reveal reveal-delay-1">`; on dark backgrounds add `section-title-light`.
- **Gold divider**: `<div class="gold-rule reveal ...">`.
- **Service cards**: `.service-card` with `.service-num`, `.service-icon`, `.service-title`, `.service-body`.
- **Stat band**: `.stat-card` with `.stat-num` + `.stat-label`.
- Respect the light-section / dark-section alternation; use `--cream` vs `--cream-dk` for adjacent light sections.

## Do / don't

- ✅ Use existing tokens and component classes; extend the `:root` palette rather than hardcoding.
- ✅ Keep copy formal and understated (see the `edit-content` skill for voice).
- ❌ Don't introduce new fonts, bright colors, drop shadows-heavy "card" looks, or emoji in the UI.
- ❌ Don't inline raw hex where a token exists.
