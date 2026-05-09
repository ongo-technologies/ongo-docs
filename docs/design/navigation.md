---
title: Navigation & Feedback
description: Ongo navigation patterns, booking tracker, avatars, toasts, and alert banners
icon: material/compass-outline
---

# Navigation & Feedback

---

## Bottom Tab Bar (Flutter)

The primary navigation for the Customer App. Four tabs: Home, Bookings, Vendors, Profile.

### Spec

```css
.nav-bar {
  display:          flex;
  background:       var(--color-bg-surface);
  border-top:       1px solid var(--color-border-subtle);
  padding:          var(--sp-2) 0;
  box-shadow:       var(--shadow-xl);
}

.nav-tab {
  flex:             1;
  display:          flex;
  flex-direction:   column;
  align-items:      center;
  gap:              var(--sp-1);
  padding:          var(--sp-2) 0;
  font-family:      var(--font-display);
  font-size:        var(--text-xs);        /* 11px */
  font-weight:      600;
  color:            var(--color-text-tertiary);
  letter-spacing:   0.02em;
  transition:       all var(--duration-fast) var(--ease-out);
}

.nav-tab.active {
  color:            var(--color-brand-primary);  /* teal-500 */
}
```

### Flutter

```dart
BottomNavigationBar(
  selectedItemColor:   CWSColors.teal500,
  unselectedItemColor: const Color(0xFFA8B0C0),  // --pearl-400
  selectedLabelStyle:  GoogleFonts.sora(
    fontSize: 11,
    fontWeight: FontWeight.w700,
    letterSpacing: 0.02,
  ),
  unselectedLabelStyle: GoogleFonts.sora(
    fontSize: 11,
    fontWeight: FontWeight.w600,
  ),
  type:                BottomNavigationBarType.fixed,
  backgroundColor:     Colors.white,
  elevation:           16,
  items: const [
    BottomNavigationBarItem(icon: Icon(Icons.home_outlined), label: 'Home'),
    BottomNavigationBarItem(icon: Icon(Icons.list_alt), label: 'Bookings'),
    BottomNavigationBarItem(icon: Icon(Icons.search), label: 'Vendors'),
    BottomNavigationBarItem(icon: Icon(Icons.person_outline), label: 'Profile'),
  ],
)
```

---

## Booking Progress Tracker

5-step horizontal tracker shown on the booking detail screen. Reflects the booking status enum in real time.

### Steps

1. Booked
2. Confirmed
3. En Route ← active step example
4. Washing
5. Done

### Spec

```css
/* Completed step */
.tracker-step.done .tracker-dot {
  background:  var(--color-brand-primary);  /* teal-500 */
  color:       white;
}
/* Active step */
.tracker-step.active .tracker-dot {
  background:  var(--color-brand-primary);
  box-shadow:  var(--shadow-brand);
  animation:   pulse 2s infinite;
}
/* Future step */
.tracker-step.next .tracker-dot {
  background:  var(--pearl-100);
  color:       var(--color-text-tertiary);
  border:      1.5px solid var(--color-border-default);
}
/* Connector line */
.tracker-line {
  flex:        1;
  height:      2px;
  background:  var(--color-border-default);
}
.tracker-line.done {
  background:  var(--color-brand-primary);
}
```

---

## Avatars

| Size | Class | Dimensions | Use |
|------|-------|-----------|-----|
| XS | `avatar-xs` | 24×24px | Compact lists |
| SM | `avatar-sm` | 32×32px | Comment threads, small views |
| MD | `avatar-md` | 40×40px | Standard list items |
| LG | `avatar-lg` | 48×48px | Profile headers, vendor cards |

**Color convention:**

- **Teal** (`avatar-teal`) — current logged-in user
- **Gold** (`avatar-gold`) — premium vendor
- **Maroon** (`avatar-maroon`) — admin/special roles
- **Pearl** (`avatar-pearl`) — general/unknown

---

## Toast Notifications

Toasts appear at the top of the screen for 4 seconds. Stack is limited to 1 visible at a time on mobile.

### Variants

| Type | Background | Icon | Use |
|------|-----------|------|-----|
| **Info (default)** | `--teal-800` | 🚗 | Status updates, en-route |
| **Success** | `--color-success` | ✓ | Payment confirmed, booking done |
| **Error** | `--color-error` | ! | Payment failed, booking cancelled |

### Spec

```css
.toast {
  display:       flex;
  align-items:   flex-start;
  gap:           var(--sp-3);
  padding:       var(--sp-4) var(--sp-5);
  border-radius: var(--radius-xl);           /* 20px */
  background:    var(--teal-800);
  color:         white;
  box-shadow:    var(--shadow-xl);
  font-family:   var(--font-body);
  font-size:     var(--text-sm);
  /* Animate in from top */
  animation:     toastIn var(--duration-enter) var(--ease-out) forwards;
}

.toast-title {
  font-family: var(--font-display);
  font-size:   var(--text-base);
  font-weight: 700;
}
```

### Flutter

```dart
// Show toast
ScaffoldMessenger.of(context).showSnackBar(
  SnackBar(
    content: Row(
      children: [
        const Icon(Icons.directions_car, color: Colors.white),
        const SizedBox(width: 12),
        Expanded(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            mainAxisSize: MainAxisSize.min,
            children: [
              Text('Your unit is on the way',
                style: GoogleFonts.sora(
                  fontSize: 15,
                  fontWeight: FontWeight.w700,
                  color: Colors.white,
                )),
              Text('Arriving at 3:50 PM (~20 mins)',
                style: GoogleFonts.dmSans(
                  fontSize: 13,
                  color: Colors.white70,
                )),
            ],
          ),
        ),
      ],
    ),
    backgroundColor: const Color(0xFF053040),  // --teal-800
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(20),
    ),
    duration: const Duration(seconds: 4),
  ),
);
```

---

## Inline Alert Banners

Persistent banners within a screen — used for time-sensitive messages (cancellation window, SMS sent, etc.).

### Variants

| Type | Background | Border | Text color |
|------|-----------|--------|------------|
| Info | `--color-info-tint` | `--teal-100` | `--teal-700` |
| Warning | `--color-warning-tint` | `--color-warning-light` | `--color-warning` |
| Success | `--color-success-tint` | `--color-success-light` | `--color-success` |
| Error | `--color-error-tint` | `--color-error-light` | `--color-error` |

### Spec

```css
.alert-banner {
  display:       flex;
  gap:           var(--sp-2);
  align-items:   flex-start;
  padding:       var(--sp-3) var(--sp-4);
  border-radius: var(--radius-md);
  font-family:   var(--font-body);
  font-size:     var(--text-sm);
  border:        1px solid;
}

/* Example — warning */
.alert-banner.warning {
  background:    var(--color-warning-tint);
  border-color:  var(--color-warning-light);
  color:         var(--color-warning);
}

/* Bold prefix uses Sora */
.alert-banner strong {
  font-family:  var(--font-display);
  font-weight:  700;
}
```

**Examples in the app:**

- `ℹ️ SMS sent — Your confirmation has been sent to +974 5012 3456`
- `⚠️ 3 minutes left to cancel this booking at no charge.`
- `✅ Booking confirmed — NextGen AutoCare accepted your request.`
- `✕ Payment failed — Please check your card details and retry.`
