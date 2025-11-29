# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

MkDocs documentation site for CarWash Qatar - a car wash aggregator platform PRD. Uses Material for MkDocs theme with a clean, Notion-inspired design.

## Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Serve locally (http://127.0.0.1:8000)
mkdocs serve

# Build static site (outputs to ./site/)
mkdocs build --clean
```

## Architecture

- **Generator**: MkDocs with Material theme
- **Styling**: Custom CSS in `docs/stylesheets/extra.css`
- **Deployment**: GitHub Actions → GitHub Pages

### Key Files

- `mkdocs.yml` - Site config, navigation, theme settings
- `docs/stylesheets/extra.css` - Custom styles (Notion-inspired design)
- `requirements.txt` - Python dependencies

### Navigation Structure

```
Home
├── Product
│   ├── Overview
│   ├── Architecture
│   └── Roadmap
├── Development
│   ├── Requirements
│   └── User Stories
└── Reference
    ├── Style Guide
    └── Contributing
```

## Design System

The site uses a clean, minimal design inspired by Notion and Docusaurus:

- **Colors**: Fresh blues (`#0066FF` primary), clean grays, teal accents
- **Font**: Inter for text, JetBrains Mono for code
- **Components**: Cards, stat grids, hero sections, timelines

## Content Guidelines

- Keep content concise and scannable
- Use Qatar-specific conventions: QAR currency, kilometers, Friday-Saturday weekend
- Diagrams use Mermaid syntax
- Follow style guide in `docs/style-guide.md`
