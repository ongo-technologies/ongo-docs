---
title: Developer Tokens
description: Copy-ready SCSS, Flutter Dart, and RTL implementation tokens for CWS Qatar Design System v2.1, including full dark mode blocks
icon: material/code-tags
---

# Developer Tokens

Copy-ready snippets for Angular SCSS and Flutter Dart. These are the exact translation of the CSS tokens into each platform's theming system.

---

## Angular / SCSS

```scss
// styles/tokens/_colors.scss
// CWS Qatar Design System v2.1 — Direction B: Gulf Teal
// Light mode (:root) + Dark mode ([data-theme="dark"])

:root {
  // ── Gulf Teal (Primary) ──────────────────────────
  --teal-500: #0B8FBF;   /* ★ Primary CTA */
  --teal-700: #084E63;   /* Hover / dark bg */
  --teal-75:  #DCF7FD;   /* Selected tint */
  --teal-25:  #F5FCFF;   /* Subtle surface */

  // ── Desert Gold (Accent) ─────────────────────────
  --gold-400: #DEB84D;   /* Ratings · Pay CTA */
  --gold-600: #A97D1E;   /* Text on light bg */

  // ── Qatar Maroon (Heritage) ──────────────────────
  --maroon-700: #6B2535; /* Campaigns only */

  // ── Semantic tokens ──────────────────────────────
  --color-brand-primary:   var(--teal-500);
  --color-brand-accent:    var(--gold-400);
  --color-brand-heritage:  var(--maroon-700);

  --color-text-primary:    #1E2025;
  --color-text-secondary:  #636A78;
  --color-text-tertiary:   #A8B0C0;

  --color-bg-page:         #F8F9FB;
  --color-bg-surface:      #FFFFFF;
  --color-bg-raised:       #FFFFFF;
  --color-bg-sunken:       #F0F2F6;

  --color-border-subtle:   #F0F2F6;
  --color-border-default:  #E0E4EC;

  --color-success:         #1A7A4A;
  --color-warning:         #B87108;
  --color-error:           #C0242C;

  --shadow-brand: 0 4px 20px rgba(11,143,191,.28);
  --shadow-focus: 0 0 0 3px rgba(11,143,191,.22);
}

// ── Dark mode token overrides ─────────────────────
// Apply [data-theme="dark"] on <html> or <body>.
// Primitives are unchanged — only semantic tokens shift.
[data-theme="dark"] {
  --color-brand-primary:        #0FA8D4;   /* teal-400 — brighter for WCAG AA on dark */
  --color-brand-primary-dark:   #3DC6E8;   /* teal-300 — hover on dark */
  --color-brand-primary-light:  #053040;   /* teal-800 — tinted surface */
  --color-brand-accent:         #DEB84D;   /* gold-400 — unchanged, glows on dark */
  --color-brand-accent-dark:    #EAD07A;   /* gold-300 — hover on dark */
  --color-brand-accent-light:   #332600;   /* gold-900 — tinted surface */
  --color-brand-heritage:       #C24E68;   /* maroon-400 — readable on dark bg */

  --color-text-primary:         #E8EAEE;   /* soft white — not pure white */
  --color-text-secondary:       #9BA3B4;
  --color-text-tertiary:        #5C6370;
  --color-text-link:            #3DC6E8;   /* teal-300 — visible on dark */
  --color-text-link-hover:      #7DDCF3;   /* teal-200 */

  --color-bg-page:              #0C0F12;   /* deepest — page canvas */
  --color-bg-surface:           #141820;   /* cards, panels */
  --color-bg-raised:            #1C2029;   /* elevated cards */
  --color-bg-sunken:            #0A0D10;   /* inputs, inset areas */
  --color-bg-brand-tint:        #053040;   /* teal-800 */
  --color-bg-accent-tint:       #332600;   /* gold-900 */

  --color-border-subtle:        #1E2430;
  --color-border-default:       #262D3A;
  --color-border-strong:        #353D4D;
  --color-border-focus:         #3DC6E8;

  --color-success:              #22A060;
  --color-success-light:        #0D3D26;
  --color-warning:              #D4860F;
  --color-warning-light:        #3D2800;
  --color-error:                #E04040;
  --color-error-light:          #3D0F0F;

  /* Luminous glows — not drop shadows (OLED physics) */
  --shadow-brand: 0 4px 24px rgba(15,168,212,.35), 0 0 12px rgba(15,168,212,.15);
  --shadow-gold:  0 4px 24px rgba(222,184,77,.30),  0 0 12px rgba(222,184,77,.12);
  --shadow-focus: 0 0 0 3px rgba(61,198,232,.30);
}

// ── Angular Material override ─────────────────────
@use '@angular/material' as mat;

$cws-primary: mat.define-palette((
  50:  #EDF9FD, 100: #B5EEFA,
  200: #7DDCF3, 300: #3DC6E8,
  400: #0FA8D4, 500: #0B8FBF,
  600: #0A6882, 700: #084E63,
  800: #053040, 900: #031D26,
  contrast: (500: white, 600: white, 700: white)
), 500, 300, 700);

$cws-accent: mat.define-palette((
  400: #DEB84D, 500: #C99A2E,
  contrast: (400: #1C1500, 500: #1C1500)
), 400);
```

---

## Flutter / Dart

```dart
// lib/theme/cws_theme.dart
// CWS Qatar Design System v2.0

import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

abstract class CWSColors {
  // Gulf Teal — Primary
  static const teal500 = Color(0xFF0B8FBF);   // ★ Primary
  static const teal700 = Color(0xFF084E63);
  static const teal75  = Color(0xFFDCF7FD);
  static const teal25  = Color(0xFFF5FCFF);

  // Desert Gold — Accent
  static const gold400  = Color(0xFFDEB84D);  // ★ Accent
  static const gold600  = Color(0xFFA97D1E);

  // Qatar Maroon — Heritage
  static const maroon700 = Color(0xFF6B2535); // campaigns only

  // Pearl Neutrals
  static const pearl900 = Color(0xFF1E2025);
  static const pearl600 = Color(0xFF636A78);
  static const pearl400 = Color(0xFFA8B0C0);
  static const pearl100 = Color(0xFFF0F2F6);

  // Semantic
  static const success = Color(0xFF1A7A4A);
  static const warning = Color(0xFFB87108);
  static const error   = Color(0xFFC0242C);

  // Tints
  static const successTint = Color(0xFFF0FAF5);
  static const warningTint = Color(0xFFFFFBEB);
  static const errorTint   = Color(0xFFFFF5F5);
}

class CWSTheme {
  static ThemeData get light => ThemeData(
    useMaterial3: true,
    colorScheme: ColorScheme.fromSeed(
      seedColor: CWSColors.teal500,
      primary:   CWSColors.teal500,
      secondary: CWSColors.gold400,
      error:     CWSColors.error,
      surface:   Colors.white,
      background: const Color(0xFFF8F9FB),  // --pearl-50
    ),
    textTheme: GoogleFonts.soraTextTheme().copyWith(
      bodyMedium: GoogleFonts.dmSans(fontSize: 15),
      bodySmall:  GoogleFonts.dmSans(fontSize: 13),
    ),
    elevatedButtonTheme: ElevatedButtonThemeData(
      style: ElevatedButton.styleFrom(
        backgroundColor: CWSColors.teal500,
        foregroundColor: Colors.white,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(12),  // --radius-md
        ),
        padding: const EdgeInsets.symmetric(
          horizontal: 20, vertical: 13),
      ),
    ),
  );

  // ── Dark theme ────────────────────────────────────────────────────────────
  // Surfaces use layered depth — not flat black.
  // Teal shifts to teal-400 for WCAG AA contrast on dark backgrounds.
  // Shadows become luminous glows (OLED physics).
  static ThemeData get dark => ThemeData(
    useMaterial3: true,
    brightness: Brightness.dark,
    colorScheme: ColorScheme.dark(
      primary:    const Color(0xFF0FA8D4),  // teal-400
      secondary:  CWSColors.gold400,        // gold-400 — unchanged
      error:      const Color(0xFFE04040),  // brighter red on dark
      surface:    const Color(0xFF141820),  // --color-bg-surface
      background: const Color(0xFF0C0F12),  // --color-bg-page
      onPrimary:  const Color(0xFF111418),
      onSurface:  const Color(0xFFE8EAEE),  // soft white text
    ),
    scaffoldBackgroundColor: const Color(0xFF0C0F12),
    cardColor: const Color(0xFF141820),
    dividerColor: const Color(0xFF262D3A),
    textTheme: GoogleFonts.soraTextTheme(ThemeData.dark().textTheme).copyWith(
      bodyMedium: GoogleFonts.dmSans(
        fontSize: 15, color: const Color(0xFFE8EAEE)),
      bodySmall: GoogleFonts.dmSans(
        fontSize: 13, color: const Color(0xFF9BA3B4)),
    ),
    elevatedButtonTheme: ElevatedButtonThemeData(
      style: ElevatedButton.styleFrom(
        backgroundColor: const Color(0xFF0FA8D4),  // teal-400 on dark
        foregroundColor: const Color(0xFF111418),
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(12),
        ),
        padding: const EdgeInsets.symmetric(
          horizontal: 20, vertical: 13),
      ),
    ),
  );
}
```

To wire both themes in `main.dart`:

```dart
MaterialApp(
  theme:      CWSTheme.light,
  darkTheme:  CWSTheme.dark,
  themeMode:  ThemeMode.system,  // or ThemeMode.dark / ThemeMode.light
  // ...
)
```

---

## RTL / Arabic

```dart
// Flutter: main.dart
MaterialApp(
  locale: Locale('ar', 'QA'),
  supportedLocales: const [
    Locale('en', 'US'),
    Locale('ar', 'QA'),
  ],
  theme: CWSTheme.light,
  // Auto-mirrors layout for RTL locales
)

// Arabic font
// pubspec.yaml: google_fonts: ^6.1.0
// Use: GoogleFonts.notoKufiArabic()
// Weight 400 (body), 600 (label), 700 (heading)
// line-height: 1.9 for Arabic body copy
// Minimum font-size: 14px (Arabic legibility)
```

```scss
// Angular: app.module.ts
import { LOCALE_ID } from '@angular/core';
import { registerLocaleData } from '@angular/common';
import localeAr from '@angular/common/locales/ar-QA';
registerLocaleData(localeAr);

providers: [
  { provide: LOCALE_ID, useValue: 'ar-QA' }
]

// SCSS: direction-aware utilities
[dir="rtl"] {
  font-family: var(--font-arabic);
  text-align:  right;
  direction:   rtl;

  // Flip horizontal spacing in RTL
  .icon-left  { margin-left:  0; margin-right: var(--sp-2); }
  .icon-right { margin-right: 0; margin-left:  var(--sp-2); }
}
```

---

## Booking Status Enum Map

Direct mapping from `booking_status` DB enum to design token:

```dart
// Flutter
Color statusColor(String status) {
  switch (status) {
    case 'pending':     return CWSColors.warning;       // #B87108
    case 'confirmed':   return CWSColors.success;       // #1A7A4A
    case 'assigned':    return CWSColors.teal500;       // #0B8FBF
    case 'en_route':    return const Color(0xFF0A6882); // teal-600
    case 'arrived':     return CWSColors.teal700;       // #084E63
    case 'in_progress': return const Color(0xFF0FA8D4); // teal-400
    case 'completed':   return CWSColors.success;       // #1A7A4A
    case 'cancelled':   return CWSColors.error;         // #C0242C
    case 'rejected':    return CWSColors.error;         // #C0242C
    case 'refunded':    return CWSColors.pearl600;      // #636A78
    default:            return CWSColors.pearl400;
  }
}
```

```scss
// Angular: SCSS utility classes
.status-pending     { color: var(--color-warning); }
.status-confirmed   { color: var(--color-success); }
.status-assigned    { color: var(--teal-500); }
.status-en_route    { color: var(--teal-600); }
.status-arrived     { color: var(--teal-700); }
.status-in_progress { color: var(--teal-400); }
.status-completed   { color: var(--color-success); }
.status-cancelled   { color: var(--color-error); }
.status-rejected    { color: var(--color-error); }
.status-refunded    { color: var(--pearl-600); }
```
