---
title: Contributing
description: How to contribute to CarWash Qatar documentation
icon: material/hand-heart-outline
---

# Contributing

## Quick Start

1. Clone the repository
2. Install dependencies: `pip install -r requirements.txt`
3. Run locally: `mkdocs serve`
4. Make changes in `docs/` directory
5. Submit a pull request

## File Structure

```
docs/
├── index.md              # Home page
├── product/
│   ├── overview.md       # Product vision
│   ├── architecture.md   # Tech stack
│   └── roadmap.md        # Milestones
├── development/
│   ├── requirements.md   # Specs
│   └── user-stories.md   # Epics
├── style-guide.md        # Writing standards
└── contributing.md       # This file
```

## Making Changes

### Adding a New Page

1. Create a `.md` file in the appropriate folder
2. Add front matter:
   ```yaml
   ---
   title: Page Title
   description: Brief description
   ---
   ```
3. Add to `nav` in `mkdocs.yml`

### Editing Existing Pages

1. Edit the file directly
2. Preview locally with `mkdocs serve`
3. Commit with a clear message

## Pull Request Guidelines

- One topic per PR
- Clear, descriptive title
- Brief description of changes
- Ensure local build passes

## Review Process

1. Submit PR
2. Automated checks run
3. Team reviews content
4. Merge after approval
5. Auto-deploys to GitHub Pages

## Need Help?

- Check [MkDocs documentation](https://www.mkdocs.org/)
- Review [Material theme docs](https://squidfunk.github.io/mkdocs-material/)
- Open an issue for questions
