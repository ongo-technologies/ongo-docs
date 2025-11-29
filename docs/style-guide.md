---
title: Style Guide
description: Writing and formatting standards for CarWash Qatar documentation
icon: material/palette-outline
---

# Style Guide

## Writing Principles

- **Clarity first**: Simple language, avoid jargon
- **Active voice**: "The system processes payments" not "Payments are processed"
- **Concrete examples**: Use Qatar-specific scenarios
- **Professional tone**: Approachable but confident

## Qatar-Specific Standards

### Currency
- Primary: **QAR 150** (always show QAR first)
- With conversion: QAR 150 (~$40 USD)
- Use commas: QAR 1,500

### Geography
- Locations: Doha, West Bay, Pearl Qatar, Al Rayyan
- Distances: Kilometers (25km, not miles)
- Coverage terms: "Greater Doha area", "Qatar metro region"

### Cultural Elements
- **Prayer times**: Automatic integration required
- **Weekend**: Friday-Saturday pattern
- **Holidays**: Eid, National Day, Ramadan
- **Business hours**: Respect local timing preferences

### Language
- English primary, Arabic secondary
- Plan for RTL layout
- Use Qatar-specific business terms

## Formatting

### Headings
```markdown
# Document Title (H1 - once per page)
## Major Section (H2)
### Subsection (H3)
#### Detail (H4)
```

### Code Blocks
Always specify language:
```python
def process_booking():
    return "Booking confirmed"
```

### Tables
| Column 1 | Column 2 |
|----------|----------|
| Data     | Data     |

### Lists
Use ordered lists for sequential steps, unordered for features.

## Diagrams

Use Mermaid syntax:

```mermaid
graph LR
    A[Start] --> B[Process] --> C[End]
```

## Quality Checklist

Before submitting:

- [ ] Qatar market relevance
- [ ] Cultural considerations included
- [ ] Technical accuracy verified
- [ ] QAR currency shown first
- [ ] Links work correctly
