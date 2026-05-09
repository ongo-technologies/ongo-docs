---
title: Buttons & Badges
description: Ongo button variants, sizes, badge and status chip system
icon: material/cursor-default-click-outline
---

# Buttons & Badges

---

## Buttons

Six variants, four sizes. **Max one primary CTA per screen.** Gold is reserved for payment/confirmation actions only.

### Variants

| Variant | Class | Token | Use |
|---------|-------|-------|-----|
| **Primary** | `btn-primary` | `--color-brand-primary` (teal-500) | Main booking action — one per screen |
| **Gold / Pay** | `btn-gold` | `--color-brand-accent` (gold-400) | "Confirm & Pay" — payment confirmation only |
| **Outline** | `btn-outline` | `--color-brand-primary` border | Secondary actions, "View All" |
| **Ghost** | `btn-ghost` | `--color-text-secondary` | Tertiary actions, "Cancel" |
| **Danger** | `btn-danger` | `--color-error` | Destructive actions — "Reject Job", "Delete" |
| **Heritage** | `btn-heritage` | `--color-brand-heritage` (maroon-700) | Qatar National Day / Ramadan promotions only |

### Sizes

| Size | Height | Padding | Font | Use |
|------|--------|---------|------|-----|
| `btn-xl` | 56px | 24px horizontal | Sora 700, 17px | Hero CTAs, splash screen |
| `btn-lg` | 48px | 20px horizontal | Sora 700, 15px | Primary booking actions |
| `btn-md` | 40px | 16px horizontal | Sora 600, 14px | Standard UI buttons |
| `btn-sm` | 32px | 12px horizontal | Sora 600, 12px | Compact / inline actions |

### Spec

```css
/* Primary button */
background:    var(--color-brand-primary);   /* #0B8FBF */
color:         var(--color-text-inverse);    /* white */
border-radius: var(--radius-md);             /* 12px */
box-shadow:    var(--shadow-brand);          /* teal glow */
font-family:   var(--font-display);          /* Sora */
font-weight:   700;
transition:    all var(--duration-base) var(--ease-out);

/* Hover */
background:    var(--color-brand-primary-dark);  /* teal-700 */
transform:     translateY(-1px);
box-shadow:    var(--shadow-lg);

/* Gold / Pay button */
background:    var(--color-brand-accent);    /* #DEB84D */
color:         #1C1500;                      /* pearl-950 — dark text on gold */
box-shadow:    var(--shadow-gold);
```

### Flutter

```dart
// Primary button
ElevatedButton(
  style: ElevatedButton.styleFrom(
    backgroundColor: CWSColors.teal500,
    foregroundColor: Colors.white,
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(12),
    ),
    padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 13),
    elevation: 4,
    shadowColor: CWSColors.teal500.withOpacity(0.28),
  ),
  onPressed: () {},
  child: const Text('Book Now'),
)

// Gold/Pay button
ElevatedButton(
  style: ElevatedButton.styleFrom(
    backgroundColor: CWSColors.gold400,
    foregroundColor: const Color(0xFF1C1500),
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(12),
    ),
  ),
  onPressed: () {},
  child: const Text('Confirm & Pay — QAR 45'),
)
```

---

## Badges & Status Chips

Status chips map directly to the booking status enum. Use the exact variant names to keep Flutter and Angular in sync.

### Variants

| Variant | Background | Text | Dot color | Use |
|---------|-----------|------|-----------|-----|
| `bdg-success` | `--color-success-tint` | `--color-success` | `#1A7A4A` | Confirmed, Completed |
| `bdg-warning` | `--color-warning-tint` | `--color-warning` | `#B87108` | Pending, Awaiting |
| `bdg-error` | `--color-error-tint` | `--color-error` | `#C0242C` | Cancelled, Rejected |
| `bdg-info` | `--color-info-tint` | `--color-info` | `#0B8FBF` | En Route |
| `bdg-brand` | `--teal-75` | `--teal-700` | `--teal-400` | In Progress, service tags |
| `bdg-gold` | `--gold-100` | `--gold-600` | `--gold-500` | Premium, VIP vendor |
| `bdg-neutral` | `--pearl-100` | `--pearl-600` | `--pearl-400` | Refunded, inactive |

### Spec

```css
/* Badge base */
display:        inline-flex;
align-items:    center;
gap:            var(--sp-1-5);          /* 6px */
padding:        3px 10px 3px 8px;
border-radius:  var(--radius-full);     /* 9999px */
font-family:    var(--font-display);    /* Sora */
font-size:      var(--text-xs);         /* 11px */
font-weight:    600;
letter-spacing: 0.02em;

/* Status dot */
.badge-dot {
  width:         6px;
  height:        6px;
  border-radius: 50%;
  flex-shrink:   0;
}
```

### Flutter

```dart
// Status badge widget
Container(
  padding: const EdgeInsets.symmetric(horizontal: 10, vertical: 3),
  decoration: BoxDecoration(
    color: CWSColors.successTint,
    borderRadius: BorderRadius.circular(9999),
  ),
  child: Row(
    mainAxisSize: MainAxisSize.min,
    children: [
      Container(
        width: 6, height: 6,
        decoration: const BoxDecoration(
          color: CWSColors.success,
          shape: BoxShape.circle,
        ),
      ),
      const SizedBox(width: 6),
      Text(
        'Confirmed',
        style: GoogleFonts.sora(
          fontSize: 11,
          fontWeight: FontWeight.w600,
          color: CWSColors.success,
        ),
      ),
    ],
  ),
)
```
