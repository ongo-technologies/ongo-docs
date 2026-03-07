---
title: Contributing
description: Internal guide for updating and maintaining CWS Qatar documentation
icon: material/hand-heart-outline
---

# Contributing to CWS Docs

This guide covers how the internal team can update and maintain the CarWash Qatar documentation site.

## Prerequisites

- Python 3.10+
- Git access to the `cws-docs` repository

## Local Development

```bash
# Clone the repo
git clone <repo-url> && cd cws-docs

# Install dependencies
pip install -r requirements.txt

# Start local dev server at http://127.0.0.1:8000
zensical serve

# Build the static site (outputs to ./site/)
zensical build
```

## File Structure

```
docs/
├── index.md                    # Home page
├── product/
│   ├── overview.md             # Product vision & goals
│   ├── architecture.md         # Technical architecture
│   └── roadmap.md              # Release milestones
├── development/
│   ├── requirements.md         # Functional & non-functional specs
│   ├── user-stories.md         # Epics & user stories
│   └── database-schema.md      # Database schema reference
├── design/
│   ├── index.md                # Design system overview
│   ├── colors.md               # Color palette
│   ├── typography.md           # Type scale & fonts
│   ├── spacing.md              # Spacing & border radius tokens
│   ├── motion.md               # Animation guidelines
│   ├── buttons.md              # Buttons & badges
│   ├── forms.md                # Form controls
│   ├── navigation.md           # Navigation & feedback components
│   └── developer-tokens.md     # Design tokens for developers
├── legal/
│   ├── privacy-policy.md       # Privacy policy
│   └── terms-and-conditions.md # Terms & conditions
├── style-guide.md              # Writing & content standards
├── contributing.md             # This file
└── stylesheets/
    └── extra.css               # Custom site styles
```

## Adding a New Page

1. Create a Markdown file in the appropriate folder under `docs/`.
2. Add front matter at the top of the file:
   ```yaml
   ---
   title: Page Title
   description: Brief description of the page
   ---
   ```
3. Register the page in the `nav` section of `zensical.toml`.
4. Preview locally with `zensical serve` before committing.

## Editing Existing Pages

1. Edit the `.md` file directly.
2. Preview with `zensical serve` to verify rendering.
3. Commit with a clear, descriptive message.

## Content Guidelines

- Follow the conventions in the [Style Guide](style-guide.md).
- Use Qatar-specific standards: QAR for currency, kilometers for distance, Friday-Saturday weekend.
- Use [Mermaid](https://mermaid.js.org/) for diagrams.
- Keep content concise and scannable -- use headings, bullet points, and tables.

## Configuration

The site is configured via `zensical.toml`. Key sections:

| Section | Purpose |
|---|---|
| `[project]` | Site name, URL, copyright |
| `nav` | Navigation structure and page ordering |
| `[project.theme]` | Theme features, fonts, color palette |
| `[project.markdown_extensions.*]` | Markdown extensions and plugins |

## Deployment

The site deploys automatically to GitHub Pages via GitHub Actions when changes are pushed to the `main` branch. Ensure `zensical build` succeeds locally before pushing.
