---
title: Developer Tokens
description: Copy-ready SCSS, Flutter Dart, and RTL implementation tokens for CWS Qatar Design System v2.0
icon: material/code-tags
---

# Developer Tokens

Copy-ready snippets for Angular SCSS and Flutter Dart. These are the exact translation of the CSS tokens into each platform's theming system.

---

## Angular / SCSS

```scss
// styles/tokens/_colors.scss
// CWS Qatar Design System v2.0 — Direction B: Gulf Teal

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

  --color-success:         #1A7A4A;
  --color-warning:         #B87108;
  --color-error:           #C0242C;

  --shadow-brand: 0 4px 20px rgba(11,143,191,.28);
  --shadow-focus: 0 0 0 3px rgba(11,143,191,.22);
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
}
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
