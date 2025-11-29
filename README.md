# CarWash Qatar - Documentation

Product documentation for Qatar's car wash aggregator platform.

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Serve locally
mkdocs serve

# Build
mkdocs build
```

View at http://127.0.0.1:8000

## Structure

```
docs/
├── index.md              # Home page
├── product/
│   ├── overview.md       # Product vision & objectives
│   ├── architecture.md   # Tech stack & system design
│   └── roadmap.md        # Development milestones
├── development/
│   ├── requirements.md   # Functional & non-functional specs
│   └── user-stories.md   # Epics & user stories
├── style-guide.md        # Documentation standards
└── contributing.md       # How to contribute
```

## Tech Stack

- **MkDocs** with Material theme
- **GitHub Pages** for hosting
- **GitHub Actions** for deployment

## Contributing

1. Edit files in `docs/`
2. Preview with `mkdocs serve`
3. Submit a pull request

See [Contributing Guide](docs/contributing.md) for details.
