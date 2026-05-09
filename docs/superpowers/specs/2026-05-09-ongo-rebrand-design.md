# Ongo Rebrand — Design Spec

**Date:** 2026-05-09
**Status:** Approved
**Scope:** cws-docs repository only (documentation site)

---

## Goal

Replace all "CarWash Qatar" / "CWS" brand references with "Ongo" across the entire documentation site. Apply a targeted voice refresh to the 6 highest-visibility strings so the brand reads as intentional, not just renamed. Introduce the O-Flow custom SVG icon as the site logo.

---

## Out of Scope

- Color palette names (Gulf Teal, Desert Gold, Qatar Maroon, Gulf Pearl) — unchanged
- CSS token values and variable names (`--teal-500`, `--gold-400`, etc.) — unchanged
- Design system version number (v2.1) — unchanged
- Geographic/Qatar context in content — unchanged (product still operates in Qatar)
- Dart/SCSS class logic — only names in documentation code snippets change, not actual source code

---

## Section 1 — Mechanical Substitutions

These are applied as exact string replacements across all matched files.

| Pattern | Replacement | Notes |
|---|---|---|
| `CarWash Qatar` | `Ongo` | All occurrences in all files |
| `CWS Qatar` | `Ongo` | All occurrences |
| `CWS` (standalone) | `Ongo` | Only where used as a brand name (e.g. "CWS app", "all CWS surfaces"). Does NOT apply to CSS variable names, color token names, or any string where CWS is not acting as a brand identifier. |
| `cws_theme.dart` | `ongo_theme.dart` | File path reference in developer-tokens.md |
| `CWSColors` | `OngoColors` | Dart class name in developer-tokens.md code snippet |
| `CWSTheme` | `OngoTheme` | Dart class name in developer-tokens.md code snippet |
| `$cws-primary` | `$ongo-primary` | SCSS variable in developer-tokens.md code snippet |
| `$cws-accent` | `$ongo-accent` | SCSS variable in developer-tokens.md code snippet |
| `cws-docs` | `ongo-docs` | Docker service name in docker-compose.yaml |
| `CarWash Qatar Team` | `Ongo Team` | zensical.toml author field |
| `© 2025 CarWash Qatar` | `© 2025 Ongo` | zensical.toml copyright |

### Files receiving mechanical substitutions

| File | Brand tokens present |
|---|---|
| `zensical.toml` | site_name, site_author, copyright |
| `README.md` | Title, description |
| `docker-compose.yaml` | Service name `cws-docs` |
| `docs/index.md` | Hero h1, hero tagline, description frontmatter |
| `docs/product/index.md` | Description frontmatter, intro paragraph |
| `docs/product/overview.md` | Description frontmatter |
| `docs/product/architecture.md` | Any CWS/CarWash mentions |
| `docs/product/roadmap.md` | Description frontmatter |
| `docs/development/index.md` | Any CWS/CarWash mentions |
| `docs/development/requirements.md` | Description frontmatter, "CWS Feature List" reference, "CWS platforms" |
| `docs/development/api-endpoints.md` | Any CWS/CarWash mentions |
| `docs/development/database-schema.md` | Any CWS/CarWash mentions |
| `docs/design/index.md` | Hero h1, hero blurb ("CWS Qatar Design System v2.1") |
| `docs/design/colors.md` | Description frontmatter |
| `docs/design/typography.md` | Any CWS mentions |
| `docs/design/spacing.md` | Any CWS mentions |
| `docs/design/motion.md` | Any CWS mentions |
| `docs/design/buttons.md` | Any CWS mentions |
| `docs/design/forms.md` | Any CWS mentions |
| `docs/design/navigation.md` | Any CWS mentions |
| `docs/design/developer-tokens.md` | Description, code comments, class names, SCSS variables, file paths |
| `docs/reference/index.md` | Any CWS/CarWash mentions |
| `docs/contributing.md` | Any CWS/CarWash mentions |
| `docs/legal/index.md` | Any CWS/CarWash mentions |
| `docs/legal/privacy-policy.md` | "CWS app" → "Ongo app" |
| `docs/legal/terms-and-conditions.md` | Any CWS/CarWash mentions |
| `reference/myfatoorah-payment-gateway.md` | Any CWS/CarWash mentions |
| `reference/cws_design_system-v2.html` | All brand mentions inside the file; **rename to `ongo-design-system-v2.html`** |
| `reference/cws_technical_plan.html` | All brand mentions inside the file; **rename to `ongo-technical-plan.html`** |
| `reference/index.md` | Update any href links pointing to the old HTML filenames |

---

## Section 2 — Voice Refresh

Targeted rewrites of 6 high-visibility strings where phrasing was shaped around the old brand name. Changes are minimal — preserve meaning, improve brand fit.

### 1. `docs/index.md` — hero tagline

```
Before: Connecting customers with professional car wash services across Qatar
After:  On-demand car wash, anywhere in Qatar
```

### 2. `zensical.toml` — site_description

```
Before: Product documentation for Qatar's car wash aggregator platform
After:  Product documentation for Ongo — Qatar's on-demand car wash platform
```

### 3. `docs/index.md` — frontmatter description

```
Before: Qatar's premier car wash aggregator platform
After:  Qatar's on-demand car wash platform
```

### 4. `docs/design/index.md` — hero blurb (after name substitution)

```
Before: The official visual language for the CWS mobile car wash platform.
        Gulf Teal primary, Desert Gold accent, Qatar Maroon as cultural heritage.
        Single source of truth for Flutter, Angular, and all CWS surfaces.

After:  The official visual language for all Ongo platforms.
        Gulf Teal primary, Desert Gold accent, Qatar Maroon as cultural heritage.
        Single source of truth for Flutter, Angular, and all Ongo surfaces.
```

### 5. `docs/product/overview.md` — Vision statement

```
Before: Qatar's leading car wash service aggregator—connecting customers with
        professional vendors through convenient on-location vehicle cleaning services.

After:  Qatar's on-demand car wash platform — connecting customers with professional
        vendors through fast, convenient vehicle cleaning at their location.
```

### 6. `docs/legal/privacy-policy.md` — app reference

```
Before: the CWS app (hereby referred to as "Application")
After:  the Ongo app (hereby referred to as "Application")
```

---

## Section 3 — O-Flow Icon

### Design

The O-Flow icon uses the "O" of Ongo as a fluid circular motion mark: a broken arc (Gulf Teal `#0B8FBF`) with a gold spray burst (Desert Gold `#DEB84D`) at the break point, and a centered dot completing the lettermark. Adapts to dark mode (teal shifts to `#0FA8D4`).

### Deliverable

- Save as: `docs/assets/ongo-icon.svg`
- SVG viewBox: `0 0 80 80`
- Colors: Gulf Teal primary arc, Desert Gold spray burst, transparent background

### Wire-in

Update `zensical.toml`:

```toml
# Before
[project.theme.icon]
logo = "material/car-wash"

# After
[project.theme.icon]
logo = "assets/ongo-icon.svg"
```

---

## Validation Checklist

After all changes are applied:

- [ ] `grep -ri "carwash\|car wash\|cws" docs/` returns zero matches (excluding color token names)
- [ ] Site serves locally with `zensical serve` without errors
- [ ] Homepage hero shows "Ongo" and updated tagline
- [ ] Nav bar shows O-Flow icon next to "Ongo" site name
- [ ] Design system page shows "Ongo Design System v2.1"
- [ ] Developer tokens page shows `ongo_theme.dart`, `OngoColors`, `OngoTheme`, `$ongo-primary`, `$ongo-accent`
- [ ] Legal docs show "Ongo app"
- [ ] Copyright footer shows "© 2025 Ongo"
- [ ] Dark mode: O-Flow icon renders correctly on dark background
- [ ] Reference HTML files contain no "CarWash Qatar" or "CWS" text

---

## Sequence

1. Save O-Flow SVG to `docs/assets/ongo-icon.svg`
2. Apply mechanical substitutions file by file (per table above)
3. Apply voice refresh strings (per Section 2)
4. Update `zensical.toml` icon path
5. Run validation checklist
6. Commit
