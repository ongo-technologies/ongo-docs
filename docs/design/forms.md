---
title: Form Controls
description: CWS Qatar input fields, states, validation, and focus ring specification
icon: material/text-box-outline
---

# Form Controls

---

## Input States

| State | Border | Background | Shadow |
|-------|--------|-----------|--------|
| **Default** | `--color-border-default` (pearl-200) | `--color-bg-surface` | `--shadow-xs` |
| **Focus** | `--teal-400` (1.5px) | `--color-bg-surface` | `--shadow-focus` |
| **Error** | `--color-error` (1.5px) | `--color-error-tint` | `--shadow-xs` |
| **Success** | `--color-success` (1.5px) | `--color-success-tint` | `--shadow-xs` |
| **Disabled** | `--color-border-subtle` | `--color-bg-sunken` | none |

### Focus Ring Spec

```css
/* Applied on :focus or :focus-visible */
border:     1.5px solid var(--teal-400);
box-shadow: 0 0 0 3px rgba(11, 143, 191, 0.22);
border-radius: var(--radius-md);  /* match input's border-radius */
outline:    none;
```

---

## CSS Spec

```css
.input {
  width:         100%;
  padding:       var(--sp-3) var(--sp-4);    /* 12px 16px */
  border:        1.5px solid var(--color-border-default);
  border-radius: var(--radius-md);           /* 12px */
  font-family:   var(--font-body);           /* DM Sans */
  font-size:     var(--text-base);           /* 15px */
  color:         var(--color-text-primary);
  background:    var(--color-bg-surface);
  box-shadow:    var(--shadow-xs);
  transition:    border-color var(--duration-base) var(--ease-out),
                 box-shadow   var(--duration-base) var(--ease-out);
}

.input:focus {
  border-color: var(--teal-400);
  box-shadow:   var(--shadow-focus);
  outline:      none;
}

.input.error {
  border-color: var(--color-error);
  background:   var(--color-error-tint);
}

.input.success {
  border-color: var(--color-success);
  background:   var(--color-success-tint);
}

.input:disabled {
  opacity:      0.5;
  cursor:       not-allowed;
  background:   var(--color-bg-sunken);
}

/* Form label */
.form-label {
  font-family:    var(--font-display);   /* Sora */
  font-size:      var(--text-xs);        /* 11px */
  font-weight:    700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color:          var(--color-text-secondary);
  margin-bottom:  var(--sp-2);           /* 8px */
}

/* Hint text */
.form-hint {
  font-family: var(--font-body);
  font-size:   var(--text-xs);
  color:       var(--color-text-tertiary);
  margin-top:  var(--sp-1);
}

/* Error message */
.form-error-msg {
  font-family: var(--font-body);
  font-size:   var(--text-xs);
  color:       var(--color-error);
  margin-top:  var(--sp-1);
}
```

---

## Flutter

```dart
// Input decoration theme
InputDecorationTheme(
  filled: true,
  fillColor: Colors.white,
  contentPadding: const EdgeInsets.symmetric(
    horizontal: 16, vertical: 12,
  ),
  border: OutlineInputBorder(
    borderRadius: BorderRadius.circular(12),
    borderSide: const BorderSide(
      color: Color(0xFFE0E4EC),  // --color-border-default
      width: 1.5,
    ),
  ),
  focusedBorder: OutlineInputBorder(
    borderRadius: BorderRadius.circular(12),
    borderSide: const BorderSide(
      color: Color(0xFF0FA8D4),  // --teal-400
      width: 1.5,
    ),
  ),
  errorBorder: OutlineInputBorder(
    borderRadius: BorderRadius.circular(12),
    borderSide: const BorderSide(
      color: Color(0xFFC0242C),  // --color-error
      width: 1.5,
    ),
  ),
  labelStyle: GoogleFonts.sora(
    fontSize: 11,
    fontWeight: FontWeight.w700,
    letterSpacing: 0.06,
  ),
  hintStyle: GoogleFonts.dmSans(
    fontSize: 15,
    color: const Color(0xFFA8B0C0),  // --color-text-tertiary
  ),
),
```

---

## Angular

```html
<!-- Standard input -->
<div class="form-group">
  <label class="form-label">Phone Number</label>
  <input class="input" type="tel" placeholder="+974 5012 3456">
</div>

<!-- Error state -->
<div class="form-group">
  <label class="form-label" [class.error-label]="hasError">OTP Code</label>
  <input class="input" [class.error]="hasError" type="text">
  <span class="form-error-msg" *ngIf="hasError">Invalid code. Please try again.</span>
</div>
```

---

## Qatar-Specific Inputs

| Field | Format | Notes |
|-------|--------|-------|
| Phone | `+974 XXXX XXXX` | Always pre-populate `+974` |
| Location | Use map picker | Text input for area name only |
| Date/Time | Qatar timezone (UTC+3) | Respect Friday-Saturday weekend |
| Currency | `QAR XX.XX` | Always prefix with QAR |
| Vehicle plate | Qatar plate format | Support alphanumeric with Arabic option |
