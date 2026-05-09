# Ongo Rebrand Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace every "CarWash Qatar" / "CWS" brand reference with "Ongo" across the cws-docs site, apply 6 targeted voice-refresh edits, and introduce the O-Flow custom SVG as the site logo.

**Architecture:** Three layers of change applied in sequence — (1) create the SVG icon asset, (2) mechanical brand substitutions across 30 files, (3) targeted voice-refresh rewrites on 6 high-visibility strings. All changes are in documentation source files only; no application code is touched.

**Tech Stack:** Zensical static site generator, Markdown, TOML config, SVG, PowerShell for grep validation

---

## File Map

| File | Change type |
|---|---|
| `docs/assets/ongo-icon.svg` | **Create** — O-Flow SVG icon |
| `zensical.toml` | Modify — site_name, site_description, site_author, copyright, icon path |
| `README.md` | Modify — title, description |
| `docker-compose.yaml` | Modify — service name |
| `docs/index.md` | Modify — frontmatter, hero h1, tagline (voice refresh) |
| `docs/product/index.md` | Modify — frontmatter, intro paragraph |
| `docs/product/overview.md` | Modify — frontmatter, vision statement (voice refresh) |
| `docs/product/architecture.md` | Modify — any CWS/CarWash mentions |
| `docs/product/roadmap.md` | Modify — frontmatter |
| `docs/development/index.md` | Modify — frontmatter, intro paragraph |
| `docs/development/requirements.md` | Modify — frontmatter, info box |
| `docs/development/api-endpoints.md` | Modify — any CWS/CarWash mentions |
| `docs/development/database-schema.md` | Modify — any CWS/CarWash mentions |
| `docs/design/index.md` | Modify — hero h1, hero blurb (voice refresh) |
| `docs/design/colors.md` | Modify — frontmatter description |
| `docs/design/typography.md` | Modify — any CWS mentions |
| `docs/design/spacing.md` | Modify — any CWS mentions |
| `docs/design/motion.md` | Modify — any CWS mentions |
| `docs/design/buttons.md` | Modify — any CWS mentions |
| `docs/design/forms.md` | Modify — any CWS mentions |
| `docs/design/navigation.md` | Modify — any CWS mentions |
| `docs/design/developer-tokens.md` | Modify — frontmatter, code comments, class names, SCSS vars, file paths |
| `docs/reference/index.md` | Modify — frontmatter, body, HTML file links |
| `docs/contributing.md` | Modify — frontmatter, body, repo name |
| `docs/legal/index.md` | Modify — frontmatter, body |
| `docs/legal/privacy-policy.md` | Modify — app name reference |
| `docs/legal/terms-and-conditions.md` | Modify — frontmatter, app name reference |
| `reference/myfatoorah-payment-gateway.md` | Modify — any CWS/CarWash mentions |
| `reference/cws_design_system-v2.html` | Rename → `ongo-design-system-v2.html` + content update |
| `reference/cws_technical_plan.html` | Rename → `ongo-technical-plan.html` + content update |

---

## Task 1: Create the O-Flow SVG Icon Asset

**Files:**
- Create: `docs/assets/ongo-icon.svg`

- [ ] **Step 1.1 — Create the assets directory if it doesn't exist**

```powershell
New-Item -ItemType Directory -Force -Path "docs/assets"
```

- [ ] **Step 1.2 — Write the O-Flow SVG file**

Create `docs/assets/ongo-icon.svg` with this exact content:

```svg
<svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M62 25 A26 26 0 1 0 63 55" stroke="#0B8FBF" stroke-width="8" stroke-linecap="round" fill="none"/>
  <circle cx="63" cy="55" r="3.5" fill="#DEB84D"/>
  <line x1="63" y1="55" x2="72" y2="46" stroke="#DEB84D" stroke-width="3" stroke-linecap="round"/>
  <line x1="63" y1="55" x2="74" y2="57" stroke="#DEB84D" stroke-width="2.5" stroke-linecap="round"/>
  <line x1="63" y1="55" x2="68" y2="65" stroke="#DEB84D" stroke-width="2" stroke-linecap="round"/>
  <circle cx="40" cy="40" r="6" fill="#0B8FBF"/>
  <circle cx="40" cy="40" r="3" fill="#EDF9FD"/>
</svg>
```

- [ ] **Step 1.3 — Verify the file exists**

```powershell
Test-Path "docs/assets/ongo-icon.svg"
```

Expected: `True`

- [ ] **Step 1.4 — Commit**

```bash
git add docs/assets/ongo-icon.svg
git commit -m "feat: add O-Flow SVG icon for Ongo brand"
```

---

## Task 2: Update Site Config (`zensical.toml`)

**Files:**
- Modify: `zensical.toml`

- [ ] **Step 2.1 — Verify old values are present**

```powershell
Select-String -Path "zensical.toml" -Pattern "CarWash Qatar|car-wash"
```

Expected: lines with `site_name`, `site_author`, `copyright`, and `logo = "material/car-wash"`

- [ ] **Step 2.2 — Apply all changes to `zensical.toml`**

Make these exact replacements:

```toml
# Line 2 — site_name
# Before:
site_name = "CarWash Qatar"
# After:
site_name = "Ongo"

# Line 4 — site_description
# Before:
site_description = "Product documentation for Qatar's car wash aggregator platform"
# After:
site_description = "Product documentation for Ongo — Qatar's on-demand car wash platform"

# Line 5 — site_author
# Before:
site_author = "CarWash Qatar Team"
# After:
site_author = "Ongo Team"

# Line 9 — copyright
# Before:
copyright = "&copy; 2025 CarWash Qatar"
# After:
copyright = "&copy; 2025 Ongo"

# Line 75 — logo icon
# Before:
logo = "material/car-wash"
# After:
logo = "assets/ongo-icon.svg"
```

- [ ] **Step 2.3 — Verify old values are gone**

```powershell
Select-String -Path "zensical.toml" -Pattern "CarWash Qatar|car-wash"
```

Expected: no output (zero matches)

- [ ] **Step 2.4 — Verify new values are present**

```powershell
Select-String -Path "zensical.toml" -Pattern "Ongo|ongo-icon"
```

Expected: matches on site_name, site_description, site_author, copyright, and logo lines

- [ ] **Step 2.5 — Commit**

```bash
git add zensical.toml
git commit -m "rebrand: update site config and icon to Ongo"
```

---

## Task 3: Update README and docker-compose

**Files:**
- Modify: `README.md`
- Modify: `docker-compose.yaml`

- [ ] **Step 3.1 — Update `README.md`**

Make these exact replacements:

```markdown
# Before (line 1):
# CarWash Qatar — Documentation

# After:
# Ongo — Documentation

# Before (line 3):
Product documentation for Qatar's car wash aggregator platform.

# After:
Product documentation for Ongo — Qatar's on-demand car wash platform.
```

- [ ] **Step 3.2 — Update `docker-compose.yaml`**

```yaml
# Before (line 4):
  cws-docs:

# After:
  ongo-docs:
```

- [ ] **Step 3.3 — Verify**

```powershell
Select-String -Path "README.md","docker-compose.yaml" -Pattern "CarWash|cws-docs"
```

Expected: no output

- [ ] **Step 3.4 — Commit**

```bash
git add README.md docker-compose.yaml
git commit -m "rebrand: update README and docker-compose to Ongo"
```

---

## Task 4: Update Homepage (`docs/index.md`)

This file has both mechanical substitutions and a voice refresh on the hero tagline.

**Files:**
- Modify: `docs/index.md`

- [ ] **Step 4.1 — Apply all changes**

```markdown
# Before — frontmatter description (line 3):
description: Qatar's premier car wash aggregator platform

# After:
description: Qatar's on-demand car wash platform

# Before — hero h1 (line 9):
  <h1>CarWash Qatar</h1>

# After:
  <h1>Ongo</h1>

# Before — hero tagline (line 10):
  <p>Connecting customers with professional car wash services across Qatar</p>

# After:
  <p>On-demand car wash, anywhere in Qatar</p>
```

- [ ] **Step 4.2 — Verify**

```powershell
Select-String -Path "docs/index.md" -Pattern "CarWash Qatar"
```

Expected: no output

- [ ] **Step 4.3 — Commit**

```bash
git add docs/index.md
git commit -m "rebrand: update homepage hero and description to Ongo"
```

---

## Task 5: Update Product Section

**Files:**
- Modify: `docs/product/index.md`
- Modify: `docs/product/overview.md`
- Modify: `docs/product/architecture.md`
- Modify: `docs/product/roadmap.md`

- [ ] **Step 5.1 — Update `docs/product/index.md`**

```markdown
# Before — frontmatter (line 3):
description: Product vision, architecture, and roadmap for CarWash Qatar

# After:
description: Product vision, architecture, and roadmap for Ongo

# Before — body (line 9):
Core product documentation for the CarWash Qatar platform — covering the vision, technical architecture, and development roadmap.

# After:
Core product documentation for the Ongo platform — covering the vision, technical architecture, and development roadmap.
```

- [ ] **Step 5.2 — Update `docs/product/overview.md`**

```markdown
# Before — frontmatter (line 3):
description: Vision, objectives, and value propositions for CarWash Qatar

# After:
description: Vision, objectives, and value propositions for Ongo

# Before — Vision statement (line 11):
Qatar's leading car wash service aggregator—connecting customers with professional vendors through convenient on-location vehicle cleaning services.

# After:
Qatar's on-demand car wash platform — connecting customers with professional vendors through fast, convenient vehicle cleaning at their location.
```

- [ ] **Step 5.3 — Update `docs/product/roadmap.md`**

```markdown
# Before — frontmatter (line 3):
description: Milestones and timeline for CarWash Qatar

# After:
description: Milestones and timeline for Ongo
```

- [ ] **Step 5.4 — Update `docs/product/architecture.md`**

Run a search first to find exact matches:

```powershell
Select-String -Path "docs/product/architecture.md" -Pattern "CarWash|CWS"
```

Replace every match of `CarWash Qatar` → `Ongo` and `CWS` (as brand name) → `Ongo`.

- [ ] **Step 5.5 — Verify the product section**

```powershell
Select-String -Path "docs/product/*.md" -Pattern "CarWash|CWS Qatar"
```

Expected: no output

- [ ] **Step 5.6 — Commit**

```bash
git add docs/product/
git commit -m "rebrand: update product section to Ongo"
```

---

## Task 6: Update Development Section

**Files:**
- Modify: `docs/development/index.md`
- Modify: `docs/development/requirements.md`
- Modify: `docs/development/api-endpoints.md`
- Modify: `docs/development/database-schema.md`

- [ ] **Step 6.1 — Update `docs/development/index.md`**

```markdown
# Before — frontmatter (line 3):
description: Development requirements and database schemas for CarWash Qatar

# After:
description: Development requirements and database schemas for Ongo

# Before — body (line 9):
Technical requirements and database schema that drive the CarWash Qatar platform.

# After:
Technical requirements and database schema that drive the Ongo platform.
```

- [ ] **Step 6.2 — Update `docs/development/requirements.md`**

```markdown
# Before — frontmatter (line 3):
description: MVP feature requirements for CarWash Qatar — organized by platform

# After:
description: MVP feature requirements for Ongo — organized by platform

# Before — info box (line 10):
    Based on **CWS Feature List MVP v4\_S** — last revised February 8, 2025, Doha, Qatar.
    This document reflects the finalized MVP scope for all four CWS platforms.

# After:
    Based on **Ongo Feature List MVP v4\_S** — last revised February 8, 2025, Doha, Qatar.
    This document reflects the finalized MVP scope for all four Ongo platforms.
```

- [ ] **Step 6.3 — Update `docs/development/api-endpoints.md` and `docs/development/database-schema.md`**

Search each file for brand mentions:

```powershell
Select-String -Path "docs/development/api-endpoints.md","docs/development/database-schema.md" -Pattern "CarWash|CWS"
```

Replace every match of `CarWash Qatar` → `Ongo` and `CWS` (brand name only) → `Ongo`.

- [ ] **Step 6.4 — Verify the development section**

```powershell
Select-String -Path "docs/development/*.md" -Pattern "CarWash|CWS Qatar"
```

Expected: no output

- [ ] **Step 6.5 — Commit**

```bash
git add docs/development/
git commit -m "rebrand: update development section to Ongo"
```

---

## Task 7: Update Design Foundations (All Design Pages Except Developer Tokens)

**Files:**
- Modify: `docs/design/index.md`
- Modify: `docs/design/colors.md`
- Modify: `docs/design/typography.md`
- Modify: `docs/design/spacing.md`
- Modify: `docs/design/motion.md`
- Modify: `docs/design/buttons.md`
- Modify: `docs/design/forms.md`
- Modify: `docs/design/navigation.md`

- [ ] **Step 7.1 — Update `docs/design/index.md`** (has voice refresh)

```markdown
# Before — hero h1 (line 11):
  <h1>CWS Qatar — Design System v2.1</h1>

# After:
  <h1>Ongo — Design System v2.1</h1>

# Before — hero blurb (line 12):
  <p>The official visual language for the CWS mobile car wash platform. Gulf Teal primary, Desert Gold accent, Qatar Maroon as cultural heritage. Single source of truth for Flutter, Angular, and all CWS surfaces.</p>

# After:
  <p>The official visual language for all Ongo platforms. Gulf Teal primary, Desert Gold accent, Qatar Maroon as cultural heritage. Single source of truth for Flutter, Angular, and all Ongo surfaces.</p>
```

- [ ] **Step 7.2 — Update `docs/design/colors.md`**

```markdown
# Before — frontmatter description (line 3):
description: CWS Qatar color system — four primitive families, semantic tokens, and booking status palette

# After:
description: Ongo color system — four primitive families, semantic tokens, and booking status palette
```

- [ ] **Step 7.3 — Update remaining design pages**

Search each file for brand mentions:

```powershell
Select-String -Path "docs/design/typography.md","docs/design/spacing.md","docs/design/motion.md","docs/design/buttons.md","docs/design/forms.md","docs/design/navigation.md" -Pattern "CarWash|CWS"
```

Replace every `CarWash Qatar` → `Ongo` and `CWS` (brand name) → `Ongo` in each matched file.

- [ ] **Step 7.4 — Verify design foundations (excluding developer-tokens.md)**

```powershell
Select-String -Path "docs/design/index.md","docs/design/colors.md","docs/design/typography.md","docs/design/spacing.md","docs/design/motion.md","docs/design/buttons.md","docs/design/forms.md","docs/design/navigation.md" -Pattern "CarWash|CWS"
```

Expected: no output

- [ ] **Step 7.5 — Commit**

```bash
git add docs/design/index.md docs/design/colors.md docs/design/typography.md docs/design/spacing.md docs/design/motion.md docs/design/buttons.md docs/design/forms.md docs/design/navigation.md
git commit -m "rebrand: update design system pages to Ongo"
```

---

## Task 8: Update Developer Tokens Page

This file has the most complex substitutions — code snippets with Dart class names, SCSS variables, and file path references.

**Files:**
- Modify: `docs/design/developer-tokens.md`

- [ ] **Step 8.1 — Verify all old values are present**

```powershell
Select-String -Path "docs/design/developer-tokens.md" -Pattern "CWS|cws_|CWSColors|CWSTheme|\$cws-"
```

Expected matches: `CWS Qatar Design System`, `$cws-primary`, `$cws-accent`, `cws_theme.dart`, `CWSColors`, `CWSTheme`

- [ ] **Step 8.2 — Apply all substitutions**

Make these exact replacements in `docs/design/developer-tokens.md`:

```
# Frontmatter description (line 3):
Before: description: Copy-ready SCSS, Flutter Dart, and RTL implementation tokens for CWS Qatar Design System v2.1, including full dark mode blocks
After:  description: Copy-ready SCSS, Flutter Dart, and RTL implementation tokens for Ongo Design System v2.1, including full dark mode blocks

# SCSS code block comment (line 17):
Before: // CWS Qatar Design System v2.1 — Direction B: Gulf Teal
After:  // Ongo Design System v2.1 — Direction B: Gulf Teal

# SCSS variable names (lines 105, 114):
Before: $cws-primary: mat.define-palette((
After:  $ongo-primary: mat.define-palette((

Before: $cws-accent: mat.define-palette((
After:  $ongo-accent: mat.define-palette((

# Flutter file path comment (line 125):
Before: // lib/theme/cws_theme.dart
After:  // lib/theme/ongo_theme.dart

# Flutter file comment (line 126):
Before: // CWS Qatar Design System v2.0
After:  // Ongo Design System v2.0

# Dart class name (line 131):
Before: abstract class CWSColors {
After:  abstract class OngoColors {

# All CWSColors references (lines 166, 167, 168, 179, 199, 298–308):
Before: CWSColors.teal500 / CWSColors.gold400 / CWSColors.error / CWSColors.success / CWSColors.warning / CWSColors.pearl600 / CWSColors.pearl400 / CWSColors.teal700
After:  OngoColors.teal500 / OngoColors.gold400 / OngoColors.error / OngoColors.success / OngoColors.warning / OngoColors.pearl600 / OngoColors.pearl400 / OngoColors.teal700

# Dart class name (line 162):
Before: class CWSTheme {
After:  class OngoTheme {

# All CWSTheme references (lines 234, 235, 253):
Before: CWSTheme.light / CWSTheme.dark
After:  OngoTheme.light / OngoTheme.dark

# MaterialApp usage comment context (line 234):
Before:   theme:      CWSTheme.light,
After:    theme:      OngoTheme.light,

Before:   darkTheme:  CWSTheme.dark,
After:    darkTheme:  OngoTheme.dark,

Before:   theme: CWSTheme.light,
After:    theme: OngoTheme.light,
```

> **Note:** Apply `CWSColors` → `OngoColors` and `CWSTheme` → `OngoTheme` as replace-all operations since the same class names appear multiple times throughout the code snippets.

- [ ] **Step 8.3 — Verify all old values are gone**

```powershell
Select-String -Path "docs/design/developer-tokens.md" -Pattern "CWS|cws_theme|\$cws-"
```

Expected: no output

- [ ] **Step 8.4 — Verify new values are present**

```powershell
Select-String -Path "docs/design/developer-tokens.md" -Pattern "Ongo|ongo_theme|OngoColors|OngoTheme|\$ongo-"
```

Expected: multiple matches covering all substituted locations

- [ ] **Step 8.5 — Commit**

```bash
git add docs/design/developer-tokens.md
git commit -m "rebrand: update developer tokens code snippets to Ongo naming"
```

---

## Task 9: Update Reference, Contributing, and Legal

**Files:**
- Modify: `docs/reference/index.md`
- Modify: `docs/contributing.md`
- Modify: `docs/legal/index.md`
- Modify: `docs/legal/privacy-policy.md`
- Modify: `docs/legal/terms-and-conditions.md`
- Modify: `reference/myfatoorah-payment-gateway.md`

- [ ] **Step 9.1 — Update `docs/reference/index.md`**

```markdown
# Before — frontmatter (line 3):
description: Contribution guidelines for CarWash Qatar

# After:
description: Contribution guidelines for Ongo

# Before — body (line 9):
Contribution guidelines for the CarWash Qatar documentation and codebase.

# After:
Contribution guidelines for the Ongo documentation and codebase.
```

- [ ] **Step 9.2 — Update `docs/contributing.md`**

```markdown
# Before — frontmatter (line 3):
description: Internal guide for updating and maintaining CWS Qatar documentation

# After:
description: Internal guide for updating and maintaining Ongo documentation

# Before — heading (line 7):
# Contributing to CWS Docs

# After:
# Contributing to Ongo Docs

# Before — body (line 9):
This guide covers how the internal team can update and maintain the CarWash Qatar documentation site.

# After:
This guide covers how the internal team can update and maintain the Ongo documentation site.

# Before — repo reference (line 14):
- Git access to the `cws-docs` repository

# After:
- Git access to the `ongo-docs` repository

# Before — clone command (line 20):
git clone <repo-url> && cd cws-docs

# After:
git clone <repo-url> && cd ongo-docs
```

- [ ] **Step 9.3 — Update `docs/legal/index.md`**

```markdown
# Before — frontmatter (line 3):
description: Legal documents and policies for CarWash Qatar

# After:
description: Legal documents and policies for Ongo

# Before — body (line 9):
Legal documentation, privacy policies, and terms of service for the CarWash Qatar platform.

# After:
Legal documentation, privacy policies, and terms of service for the Ongo platform.
```

- [ ] **Step 9.4 — Update `docs/legal/privacy-policy.md`**

```markdown
# Before — frontmatter (line 3):
description: Privacy policy for the CarWash Qatar platform

# After:
description: Privacy policy for the Ongo platform

# Before — body (line 9):
This privacy policy applies to the CWS app (hereby referred to as "Application")

# After:
This privacy policy applies to the Ongo app (hereby referred to as "Application")
```

- [ ] **Step 9.5 — Update `docs/legal/terms-and-conditions.md`**

```markdown
# Before — frontmatter (line 3):
description: Terms and conditions for the CarWash Qatar platform

# After:
description: Terms and conditions for the Ongo platform

# Before — body (line 9):
These terms and conditions apply to the CWS app (hereby referred to as "Application")

# After:
These terms and conditions apply to the Ongo app (hereby referred to as "Application")
```

- [ ] **Step 9.6 — Update `reference/myfatoorah-payment-gateway.md`**

```powershell
Select-String -Path "reference/myfatoorah-payment-gateway.md" -Pattern "CarWash|CWS"
```

Replace every `CarWash Qatar` → `Ongo` and `CWS` (brand name) → `Ongo` in matched lines.

- [ ] **Step 9.7 — Verify**

```powershell
Select-String -Path "docs/reference/index.md","docs/contributing.md","docs/legal/*.md","reference/myfatoorah-payment-gateway.md" -Pattern "CarWash|CWS Qatar"
```

Expected: no output

- [ ] **Step 9.8 — Commit**

```bash
git add docs/reference/ docs/contributing.md docs/legal/ reference/myfatoorah-payment-gateway.md
git commit -m "rebrand: update reference, contributing, and legal docs to Ongo"
```

---

## Task 10: Rename and Update Reference HTML Files

The reference HTML files must be renamed so their filenames no longer contain `cws`. Any links pointing to the old names in `docs/reference/index.md` must be updated to match.

**Files:**
- Rename: `reference/cws_design_system-v2.html` → `reference/ongo-design-system-v2.html`
- Rename: `reference/cws_technical_plan.html` → `reference/ongo-technical-plan.html`
- Modify: `docs/reference/index.md` — update any hrefs pointing to old filenames

- [ ] **Step 10.1 — Rename the HTML files**

```bash
git mv reference/cws_design_system-v2.html reference/ongo-design-system-v2.html
git mv reference/cws_technical_plan.html reference/ongo-technical-plan.html
```

- [ ] **Step 10.2 — Update brand text inside `reference/ongo-design-system-v2.html`**

```powershell
Select-String -Path "reference/ongo-design-system-v2.html" -Pattern "CarWash|CWS"
```

Replace every `CarWash Qatar` → `Ongo` and `CWS Qatar` / `CWS` (brand name) → `Ongo` in matched lines.

- [ ] **Step 10.3 — Update brand text inside `reference/ongo-technical-plan.html`**

```powershell
Select-String -Path "reference/ongo-technical-plan.html" -Pattern "CarWash|CWS"
```

Replace every `CarWash Qatar` → `Ongo` and `CWS Qatar` / `CWS` (brand name) → `Ongo` in matched lines.

- [ ] **Step 10.4 — Update any links in `docs/reference/index.md`**

```powershell
Select-String -Path "docs/reference/index.md" -Pattern "cws_design_system|cws_technical_plan"
```

If any matches: replace `cws_design_system-v2.html` → `ongo-design-system-v2.html` and `cws_technical_plan.html` → `ongo-technical-plan.html`.

- [ ] **Step 10.5 — Verify no old filenames remain**

```powershell
Get-ChildItem -Path "reference/" -Filter "cws_*"
```

Expected: no output (zero files matching `cws_*`)

- [ ] **Step 10.6 — Commit**

```bash
git add reference/ docs/reference/index.md
git commit -m "rebrand: rename and update reference HTML files to Ongo"
```

---

## Task 11: Final Validation

- [ ] **Step 11.1 — Run full brand scan across all docs**

```powershell
Select-String -Path "docs/**/*.md","reference/*.md","reference/*.html","zensical.toml","README.md","docker-compose.yaml" -Pattern "CarWash Qatar|CWS Qatar" -Recurse
```

Expected: **zero matches**

- [ ] **Step 11.2 — Check for any remaining standalone CWS brand references**

```powershell
Select-String -Path "docs/**/*.md","reference/*.md" -Pattern "\bCWS\b" -Recurse
```

Review each match. Any remaining `CWS` that is acting as a brand name (not part of a CSS token name or code construct) must be replaced with `Ongo`.

- [ ] **Step 11.3 — Verify no old reference HTML filenames remain**

```powershell
Get-ChildItem -Path "reference/" -Filter "cws_*"
```

Expected: no output

- [ ] **Step 11.4 — Verify O-Flow icon is wired in**

```powershell
Select-String -Path "zensical.toml" -Pattern "ongo-icon.svg"
```

Expected: one match on the `logo` line

- [ ] **Step 11.5 — Verify voice refresh strings are present**

```powershell
Select-String -Path "docs/index.md" -Pattern "On-demand car wash, anywhere in Qatar"
Select-String -Path "docs/product/overview.md" -Pattern "Qatar's on-demand car wash platform"
Select-String -Path "docs/design/index.md" -Pattern "official visual language for all Ongo platforms"
```

Expected: one match each

- [ ] **Step 11.6 — Clean up temporary icon concepts file**

```bash
git rm docs/ongo-icon-concepts.html
git rm ongo-icon-concepts.png
```

> If a local Python HTTP server is still running from the icon review session, stop it:
> ```powershell
> Get-Process -Name python* | Where-Object { $_.CommandLine -match "7890" } | Stop-Process
> ```

- [ ] **Step 11.7 — Final commit**

```bash
git add -A
git commit -m "rebrand: final cleanup and validation — CarWash Qatar → Ongo complete"
```

---

## Completion Criteria

- [ ] Zero occurrences of `CarWash Qatar` or `CWS Qatar` anywhere in the repo
- [ ] Zero occurrences of `cws_` file references in documentation prose
- [ ] `zensical serve` runs without errors
- [ ] Homepage hero reads "Ongo" with updated tagline
- [ ] Nav bar shows O-Flow SVG icon
- [ ] Design system page reads "Ongo Design System v2.1"
- [ ] Developer tokens show `OngoColors`, `OngoTheme`, `ongo_theme.dart`, `$ongo-primary`
- [ ] Legal docs show "Ongo app" in both privacy policy and terms
- [ ] Copyright footer shows "© 2025 Ongo"
- [ ] Reference HTML files renamed to `ongo-design-system-v2.html` and `ongo-technical-plan.html`
