---
title: Design System
description: CWS Qatar Design System v2.0 — the official visual language for all CWS platforms
icon: material/palette-outline
---

# Design System

<div class="hero">
  <h1>CWS Qatar — Design System v2.0</h1>
  <p>The official visual language for the CWS mobile car wash platform. Gulf Teal primary, Desert Gold accent, Qatar Maroon as cultural heritage. Single source of truth for Flutter, Angular, and all CWS surfaces.</p>
  <div class="hero-badges">
    <span class="hero-badge primary">v2.0 · Production</span>
    <span class="hero-badge success">Direction B Finalized</span>
    <span class="hero-badge">Flutter · Angular</span>
    <span class="hero-badge">EN · AR (RTL)</span>
  </div>
</div>

## What's in This System

<div class="card-grid">
  <div class="card">
    <div class="card-icon">🎨</div>
    <h3>Foundations</h3>
    <p>Colors, typography, spacing, radius, shadows, and motion tokens — the raw material of every UI element</p>
  </div>
  <div class="card">
    <div class="card-icon">🧩</div>
    <h3>Components</h3>
    <p>Buttons, badges, forms, cards, navigation, and feedback patterns — production-ready for Flutter and Angular</p>
  </div>
  <div class="card">
    <div class="card-icon">👨‍💻</div>
    <h3>Developer Tokens</h3>
    <p>Copy-ready SCSS and Dart snippets — the exact translation of design tokens into each platform's theming system</p>
  </div>
  <div class="card">
    <div class="card-icon">🌍</div>
    <h3>RTL / Arabic</h3>
    <p>Full bilingual support — Noto Kufi Arabic, RTL layout mirroring, and Qatar-specific locale implementation</p>
  </div>
</div>

## Design Principles

| Principle | Description |
|-----------|-------------|
| **Token-first** | Always use semantic tokens in components — never hardcode hex values. This allows brand updates without touching component code. |
| **GCC-familiar** | Rounded radius scale and interaction patterns mirror Careem and Talabat for immediate user familiarity in Qatar. |
| **Bilingual by default** | EN and AR (RTL) are first-class — layout, typography, and spacing are designed for both directions from the start. |
| **Motion with purpose** | Animation confirms actions and orients the user. Never animate for entertainment — use the minimum needed. |
| **One primary CTA** | Maximum one `--color-brand-primary` button per screen. Gold is reserved exclusively for payment/confirmation. |

---

## Do & Don't

!!! success "Do"

    - Always use `--color-brand-primary` for the single primary CTA per screen
    - Use `--gold-400` exclusively for star ratings, pricing figures, and the "Confirm & Pay" button
    - Use Maroon only for Qatar National Day, Ramadan, and formal vendor onboarding — never as a regular UI color
    - Apply `--shadow-brand` to all primary teal buttons
    - Maintain `--shadow-focus` ring on all interactive elements for accessibility
    - Use **Sora** for all headings, buttons, labels, prices — **DM Sans** for all body copy
    - Use **Noto Kufi Arabic** for all Arabic text — never Sora or DM Sans in RTL mode
    - Always mirror layouts horizontally when switching to Arabic (RTL)
    - Only reference semantic tokens in components (never raw hex values)
    - Use Pearl 900 `#1E2025` for all primary text — never pure `#000000`

!!! danger "Don't"

    - Never use Maroon as a primary color in everyday UI — it is a heritage accent only
    - Never place two primary CTA buttons side by side on the same screen
    - Never use raw hex values in component code — always use CSS variables
    - Never use Gold as a background color for large surfaces — only for accents and icons
    - Never display Arabic text using Sora or DM Sans — always switch to Noto Kufi Arabic
    - Never use pure black `#000000` or pure white `#FFFFFF` for text — use Pearl scale
    - Never disable the focus ring for accessibility reasons
    - Never use `shadow-2xl` for anything other than full-screen overlays/drawers
    - Never add a new color outside this system without design review
    - Never use Inter, Roboto, or system fonts — always load Sora and DM Sans from CDN

---

## Quick Reference

| Platform | Token file | Font setup |
|----------|-----------|------------|
| Angular | `styles/tokens/_colors.scss` | Google Fonts CDN in `index.html` |
| Flutter | `lib/theme/cws_theme.dart` | `google_fonts: ^6.1.0` in pubspec |

See [Developer Tokens](developer-tokens.md) for copy-ready implementation snippets.
