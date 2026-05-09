---
title: Typography
description: Ongo three-font system — Sora, DM Sans, and Noto Kufi Arabic
icon: material/format-font
---

# Typography

Three-font system. Sora leads all display and UI. DM Sans handles body reading. Noto Kufi Arabic serves all RTL surfaces. **Never mix fonts within the same typographic role.**

---

## Font Families

### Sora — Primary Display

```
Role:    Headings · Buttons · Labels · Prices · Nav items
Source:  Google Fonts CDN
Flutter: GoogleFonts.sora()
Weights: 300 · 400 · 500 · 600 · 700 · 800
```

Geometric terminals harmonise visually with Arabic letterforms — critical for EN/AR switching.

**Sample:**

> *Book Your Wash* — Sora 800, -0.025em tracking
>
> *QAR 45.00 — Shine Wash* — Sora 700, teal-500
>
> *CONFIRM BOOKING* — Sora 600, 0.08em tracking, uppercase

---

### DM Sans — Body / Supporting

```
Role:    Body copy · Descriptions · Help text · Form hints
Source:  Google Fonts CDN
Flutter: GoogleFonts.dmSans()
Weights: 300 · 400 · 500
```

Optically corrected for small-size screen rendering. Neutral character creates visual rest from Sora's personality during long booking flows.

**Sample:**

> *Your unit is 20 minutes away. Track status updates via SMS notification.* — DM Sans 400, 1.7 line-height
>
> *Cancellation available within 5 minutes of booking.* — DM Sans 400 italic, tertiary color

---

### Noto Kufi Arabic — للغة العربية

```
Role:    All Arabic text · RTL layouts · Bilingual labels
Source:  Google Fonts CDN
Flutter: GoogleFonts.notoKufiArabic()
Weights: 300 · 400 · 600 · 700
```

Standard for Qatar government and e-commerce apps. Full Unicode Qatari Arabic coverage. Kufi construction pairs with Sora's geometry.

**Sample:**

> *احجز الآن في أي مكان* — Noto Kufi 700, RTL, 1.5 line-height
>
> *وصول متوقع خلال ٢٠ دقيقة* — Noto Kufi 400, RTL, 1.9 line-height

---

## Type Scale

| Style | Font | Size | Weight | Tracking | Leading | Use |
|-------|------|------|--------|----------|---------|-----|
| **Hero / Display** | Sora | 56–60px | 800 | -0.03em | 1.08 | Splash · Onboarding hero |
| **H1 — Screen Title** | Sora | 36–48px | 700 | -0.025em | 1.12 | Screen headers |
| **H2 — Section** | Sora | 30px | 700 | -0.02em | 1.2 | Card headers · Modals |
| **H3 — Subsection** | Sora | 24px | 600 | -0.015em | 1.3 | Group labels · Drawer titles |
| **Body Large** | DM Sans | 17px | 400 | 0 | 1.7 | Onboarding · Long descriptions |
| **Body** | DM Sans | 15px | 400 | 0 | 1.55 | General content · Details |
| **Body Small** | DM Sans | 13px | 400 | 0 | 1.6 | Captions · Timestamps · Hints |
| **UI Label** | Sora | 11px | 600–700 | +0.08em | — | Tags · Form labels · Nav (UPPERCASE) |
| **Arabic Hero** | Noto Kufi | 36–48px | 700 | 0 | 1.5 | RTL screen headers |
| **Arabic Body** | Noto Kufi | 15–17px | 400 | 0 | 1.9 | RTL body copy |

---

## CSS Tokens

```css
--font-display: 'Sora', sans-serif;
--font-body:    'DM Sans', sans-serif;
--font-arabic:  'Noto Kufi Arabic', sans-serif;
--font-mono:    'Courier New', monospace;

/* Size scale */
--text-2xs:  10px;
--text-xs:   11px;
--text-sm:   13px;
--text-base: 15px;
--text-md:   17px;
--text-lg:   20px;
--text-xl:   24px;
--text-2xl:  30px;
--text-3xl:  36px;
--text-4xl:  48px;
--text-5xl:  60px;

/* Line heights */
--leading-tight:   1.15;
--leading-snug:    1.3;
--leading-normal:  1.55;
--leading-relaxed: 1.7;
--leading-loose:   1.9;   /* Arabic body */

/* Letter spacing */
--tracking-tight:  -0.03em;
--tracking-snug:   -0.02em;
--tracking-normal:  0;
--tracking-wide:    0.04em;
--tracking-wider:   0.08em;
--tracking-widest:  0.12em;
```

---

## Google Fonts CDN

```html
<!-- In Angular index.html or Flutter web/index.html -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@300;400;500;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&family=Noto+Kufi+Arabic:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

---

## Flutter Setup

```dart
// pubspec.yaml
dependencies:
  google_fonts: ^6.1.0

// lib/theme/cws_theme.dart
textTheme: GoogleFonts.soraTextTheme().copyWith(
  bodyMedium: GoogleFonts.dmSans(fontSize: 15),
  bodySmall:  GoogleFonts.dmSans(fontSize: 13),
),
// Arabic:
GoogleFonts.notoKufiArabic(
  fontSize: 15,
  height: 1.9,   // Arabic line-height
)
```

---

## RTL Rules

- Use `Noto Kufi Arabic` for **all** Arabic text — never Sora or DM Sans in RTL mode
- Minimum Arabic font size: **14px** for legibility
- Arabic line-height: **1.9** (Arabic scripts need more vertical breathing room)
- Always set `direction: rtl; text-align: right` for Arabic content blocks
- Mirror all horizontal icon/label spacing when switching to RTL (see [Developer Tokens](developer-tokens.md#rtl--arabic))
