---
title: Motion
description: Ongo motion tokens — durations and easing curves for Flutter and Angular
icon: material/motion-outline
---

# Motion & Transitions

Use the minimum animation necessary. In a booking app, motion should **confirm actions and orient the user** — not entertain.

---

## Duration Tokens

| Token | Value | Use |
|-------|-------|-----|
| `--duration-fast` | 150ms | Hover states, badge toggles, icon swaps |
| `--duration-base` | 220ms | Button press, card hover lift, input focus |
| `--duration-slow` | 380ms | Modal open/close, bottom sheet slide |
| `--duration-enter` | 420ms | Screen transitions, page loads, hero reveals |

```css
--duration-fast:  150ms;
--duration-base:  220ms;
--duration-slow:  380ms;
--duration-enter: 420ms;
```

---

## Easing Curves

| Token | Curve | Use |
|-------|-------|-----|
| `--ease-out` | `cubic-bezier(0.16, 1, 0.3, 1)` | Most UI transitions — elements entering the screen |
| `--ease-in-out` | `cubic-bezier(0.65, 0, 0.35, 1)` | Status transitions, progress bars |
| `--ease-spring` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Button press feedback, card selection — subtle overshoot |

```css
--ease-out:    cubic-bezier(0.16, 1, 0.3, 1);
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
--ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
```

---

## Usage Guidelines

### Entering vs Exiting

- **Enter**: `--ease-out` + `--duration-enter` — elements decelerate as they arrive
- **Exit**: `--ease-in-out` + `--duration-slow` — elements accelerate away
- **Hover/press**: `--ease-spring` + `--duration-base` — gives physical feedback

### Flutter

```dart
// Standard transition
AnimatedContainer(
  duration: const Duration(milliseconds: 220),  // --duration-base
  curve: Curves.easeOut,                        // --ease-out
)

// Screen route transition
PageRouteBuilder(
  transitionDuration: const Duration(milliseconds: 420),  // --duration-enter
  transitionsBuilder: (context, animation, _, child) {
    return FadeTransition(
      opacity: CurvedAnimation(
        parent: animation,
        curve: Curves.easeOut,
      ),
      child: child,
    );
  },
)
```

### Angular

```scss
// Button hover
.btn-primary {
  transition: all var(--duration-base) var(--ease-out);
}

// Modal entrance
.modal-enter {
  animation: slideUp var(--duration-enter) var(--ease-out) forwards;
}

// Status chip change
.badge {
  transition: background-color var(--duration-fast) var(--ease-in-out);
}
```

---

## Reduced Motion

Always respect `prefers-reduced-motion` for accessibility:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

```dart
// Flutter — check platform accessibility settings
if (!MediaQuery.of(context).disableAnimations) {
  // apply animation
}
```
