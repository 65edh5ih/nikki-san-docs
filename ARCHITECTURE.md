# Architecture — nikki-san

This document describes the **technical architecture of the nikki-san blog system**.  
It complements `AI_CONTEXT.md` by explaining **how components interact**.

---

# System Overview

The system is a **static blog platform built using Hugo** and deployed via **Cloudflare Pages**.

Architecture flow:

```text
FC2 export
↓
conversion scripts
↓
Hugo content structure
↓
Hugo static site generation
↓
GitHub repository
↓
Cloudflare Pages deployment
↓
public website
```

---

# Theme Delivery Layer

The Stack theme is integrated through **Hugo Modules**.

Example configuration:

```toml
[module]
  [[module.imports]]
    path = "github.com/CaiJimmy/hugo-theme-stack/v3"
```

Consequences:
- the repository may have **no local `themes/` directory**
- upstream theme files are resolved through the Hugo module cache
- customization should be done through local overrides under `layouts/`, `assets/`, and related project directories

This distinction is important when debugging file paths or advising where to edit theme behavior.

---

# Source Data

Original platform: FC2 Blog  
Export source file: `kiam.txt`

This file contains:
- blog entries
- metadata
- comments

---

# Migration Layer

Migration is performed using custom Python scripts.

## `fc2_export_to_hugo.py`

Purpose: Convert FC2 export data into Hugo-compatible content.

Output structure:

```text
content/posts/<POST_ID>/index.md
```

Responsibilities:
- parse FC2 export format
- extract post metadata
- convert body to Markdown
- maintain original post IDs

## `extract_comments.py`

Purpose: Extract comments from the FC2 export.

Responsibilities:
- parse comment sections
- associate comments with post IDs
- generate comment data used by Hugo

The comment data is later rendered in templates.

---

# Content Layer

Hugo content directory:

```text
content/posts/
```

Each post is structured as:

```text
content/posts/<POST_ID>/index.md
```

Example:

```text
content/posts/6256/index.md
```

Advantages of this structure:
- stable permalink
- easy asset management
- consistent mapping from FC2 entry ID

---

# Archive Generation

Archives are generated using a script.

Script:
- `rebuild_archives.py`

Generated files:
- `data/archives/months.json`
- `content/archives/YYYY/_index.md`
- `content/archives/YYYY/MM/_index.md`

The generation process is deterministic.

The script reads post metadata and builds:
- year archives
- month archives

---

# Theme Override Layer

Theme used: `hugo-theme-stack`

Theme customization includes:
- layout overrides
- CSS customization
- additional partial templates

Overrides may exist under:
- `layouts/_default/`
- `layouts/_partials/`
- `layouts/partials/`

Important note:
- For the current upstream Stack theme, some theme partials live under underscore-prefixed paths such as `layouts/_partials/footer/`.
- AI must not assume that the correct override path is always `layouts/partials/...` without checking the active theme structure.

A concrete example discovered in this project:
- footer rendering may be attached manually inside custom page templates by calling `{{ partial "footer/footer" . }}`
- therefore, not every page necessarily inherits the footer automatically from a global base template

---

# Styling Layer

Custom CSS is applied to reproduce the original FC2 blog visual style.

Typical modifications include:
- blockquote appearance
- typography adjustments
- card layout spacing
- responsive tweaks
- footer styling overrides

Custom CSS may exist in:
- `assets/scss/`
- `static/css/`

When debugging visual behavior, inspect computed styles rather than assuming whether a style comes from the theme or from custom SCSS.

---

# Rendering Layer

Hugo generates the final static site.

Command used locally:

```bash
hugo server --disableFastRender
```

Output directory:

```text
public/
```

The static site includes:
- HTML
- CSS
- JS
- images

---

# Deployment Layer

Deployment pipeline:

```text
GitHub repository
↓
Cloudflare Pages build
↓
public site
```

Cloudflare Pages automatically rebuilds the site when the repository changes.

---

# URL Compatibility

Legacy FC2 URLs:

```text
/blog-entry-XXXX.html
```

New URLs:

```text
/posts/<POST_ID>/
```

Redirect rules ensure compatibility with old links.

---

# Additional Components

The site includes additional features:
- syntax highlighting (Prism.js)
- Flickr embeds
- Google Maps embeds
- comment display templates
- latest comments page

These features are integrated through Hugo templates, generated data, or Markdown content.

---

# Design Principles

The architecture follows these principles:
- deterministic generation
- stable URL structure
- minimal runtime dependencies
- long-term maintainability
- local overrides instead of editing upstream theme sources directly

---

# When Updating Architecture

If the architecture changes significantly, update:
- `AI_CONTEXT.md`
- `ARCHITECTURE.md`
- `REPO_MAP.md`
- `KNOWN_ISSUES.md`

so that future AI sessions use the current structure rather than outdated assumptions.
