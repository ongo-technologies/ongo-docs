# CarWash Qatar — Documentation

Product documentation for Qatar's car wash aggregator platform.

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Serve locally (http://127.0.0.1:8000)
zensical serve

# Build static site
zensical build
```

## Structure

```
docs/
├── index.md
├── product/
│   ├── overview.md
│   ├── architecture.md
│   └── roadmap.md
├── development/
│   ├── requirements.md
│   ├── user-stories.md
│   └── database-schema.md
├── design/
│   ├── index.md
│   ├── colors.md
│   ├── typography.md
│   ├── spacing.md
│   ├── motion.md
│   ├── buttons.md
│   ├── forms.md
│   ├── cards.md
│   ├── navigation.md
│   └── developer-tokens.md
├── legal/
│   ├── privacy-policy.md
│   └── terms-and-conditions.md
├── style-guide.md
└── contributing.md
```

## Tech Stack

- **Zensical** static site generator
- **GitHub Pages** for hosting
- **GitHub Actions** for deployment

## Docker

```bash
docker compose up
```

Serves at http://localhost:3000
