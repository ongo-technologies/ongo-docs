---
title: Spacing & Radius
description: 8px grid spacing scale, border radius system, and elevation shadows
icon: material/ruler
---

# Spacing & Radius

---

## Spacing Scale

8px base grid. All spacing values are multiples of 4px. In Flutter use these as `double` values (e.g. `16.0`). In Angular/SCSS use the CSS variables directly.

| Token | Value | Use |
|-------|-------|-----|
| `--sp-px` | 1px | Hairlines, dividers |
| `--sp-0-5` | 2px | Icon gap micro |
| `--sp-1` | 4px | Inline micro gaps, swatch padding |
| `--sp-2` | 8px | Icon-text gap, badge padding |
| `--sp-3` | 12px | Compact list items, chip padding |
| `--sp-4` | 16px | Standard padding, row gaps, button padding |
| `--sp-5` | 20px | Card inner padding, list item height |
| `--sp-6` | 24px | Section padding, form group spacing |
| `--sp-7` | 28px | |
| `--sp-8` | 32px | Component separation, card gap |
| `--sp-9` | 36px | |
| `--sp-10` | 40px | Modal padding, nav bar height |
| `--sp-12` | 48px | Section breaks (mobile screens) |
| `--sp-14` | 56px | |
| `--sp-16` | 64px | Hero top/bottom padding |
| `--sp-20` | 80px | Page section breaks (web/tablet) |
| `--sp-24` | 96px | Large whitespace, full-bleed padding |
| `--sp-32` | 128px | |

```css
/* CSS tokens */
--sp-px:  1px;  --sp-0-5: 2px;  --sp-1:   4px;
--sp-2:   8px;  --sp-3:  12px;  --sp-4:  16px;
--sp-5:  20px;  --sp-6:  24px;  --sp-7:  28px;
--sp-8:  32px;  --sp-9:  36px;  --sp-10: 40px;
--sp-12: 48px;  --sp-14: 56px;  --sp-16: 64px;
--sp-20: 80px;  --sp-24: 96px;  --sp-32: 128px;
```

---

## Border Radius

Rounded radius scale mirrors GCC on-demand app conventions (Careem, Talabat) for immediate user familiarity.

| Token | Value | Use |
|-------|-------|-----|
| `--radius-xs` | 4px | Tags · Code chips · Micro elements |
| `--radius-sm` | 8px | Inputs · Small cards |
| `--radius-md` | 12px | Buttons · Standard cards |
| `--radius-lg` | 16px | Section cards |
| `--radius-xl` | 20px | Booking cards · Panels |
| `--radius-2xl` | 24px | Modals · Bottom sheets |
| `--radius-3xl` | 32px | Hero panels · Hero cards |
| `--radius-full` | 9999px | Pills · Badges · Avatars |

```css
--radius-xs:   4px;
--radius-sm:   8px;
--radius-md:   12px;
--radius-lg:   16px;
--radius-xl:   20px;
--radius-2xl:  24px;
--radius-3xl:  32px;
--radius-full: 9999px;
```

---

## Elevation & Shadows

Use the lowest shadow that achieves the required perceived lift. The brand and gold glows are reserved for interactive CTA buttons only.

| Token | Use |
|-------|-----|
| `--shadow-xs` | Table rows, subtle hover |
| `--shadow-sm` | Standard cards |
| `--shadow-md` | Booking cards, vendor cards |
| `--shadow-lg` | Dropdowns · Hover state elevation |
| `--shadow-xl` | Modals · Toast notifications |
| `--shadow-2xl` | Full-screen overlays / drawers only |
| `--shadow-brand` | Primary teal CTA button glow |
| `--shadow-gold` | Gold accent CTA glow |
| `--shadow-focus` | Keyboard / touch focus ring |

```css
--shadow-xs:    0 1px 2px rgba(28,32,40,.06);
--shadow-sm:    0 2px 6px rgba(28,32,40,.08), 0 1px 2px rgba(28,32,40,.04);
--shadow-md:    0 4px 16px rgba(28,32,40,.10), 0 2px 4px rgba(28,32,40,.05);
--shadow-lg:    0 8px 32px rgba(28,32,40,.12), 0 4px 8px rgba(28,32,40,.06);
--shadow-xl:    0 16px 48px rgba(28,32,40,.14), 0 8px 16px rgba(28,32,40,.07);
--shadow-2xl:   0 24px 64px rgba(28,32,40,.18), 0 12px 24px rgba(28,32,40,.08);

/* Branded glows */
--shadow-brand: 0 4px 20px rgba(11,143,191,.28), 0 1px 4px rgba(11,143,191,.12);
--shadow-gold:  0 4px 20px rgba(222,184,77,.32),  0 1px 4px rgba(222,184,77,.14);

/* Focus ring — always apply to interactive elements */
--shadow-focus: 0 0 0 3px rgba(11,143,191,.22);
```

### Focus Ring Spec

All interactive elements must implement the focus ring for WCAG AA+ accessibility:

```css
/* Focus state */
border: 1.5px solid var(--teal-400);
box-shadow: var(--shadow-focus);   /* 0 0 0 3px rgba(11,143,191,.22) */
border-radius: var(--radius-md);   /* match element's own radius */
```

!!! danger "Never disable focus rings"
    The `--shadow-focus` ring must be applied to all interactive elements. Never remove focus indicators for aesthetic reasons — this breaks keyboard navigation and WCAG compliance.

---

## Z-Index Scale

| Token | Value | Layer |
|-------|-------|-------|
| `--z-base` | 0 | Normal document flow |
| `--z-raised` | 10 | Raised cards, sticky elements |
| `--z-dropdown` | 200 | Dropdown menus |
| `--z-sticky` | 300 | Sticky headers |
| `--z-overlay` | 400 | Background overlays |
| `--z-modal` | 500 | Modals, bottom sheets |
| `--z-toast` | 600 | Toast notifications (always on top) |
