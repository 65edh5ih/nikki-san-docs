# AI Context — nikki-san (Cloudflare Pages + Hugo)

IMPORTANT  
このファイルは **AI（ChatGPTなど）がこのプロジェクトを理解するための仕様書**です。  
回答する前に必ずこのファイルの内容を前提にしてください。  
AI assistants must read all files under `docs/` before answering.

---

# Project Overview

This project is a **static blog migrated from FC2 Blog**.

Platform stack:
- Hugo static site generator
- Hugo theme: **Stack**
- Hosted on **Cloudflare Pages**
- Source repository: GitHub
- Deployment: automatic from GitHub

Primary public URL: `https://nikki-san.pages.dev/`

---

# Repository

GitHub repository: `https://github.com/65edh5ih/nikki-san`

The site is built automatically by Cloudflare Pages when the repository is updated.

---

# Theme / Module System

This project uses **Hugo Modules** for the theme, not the legacy `themes/` directory workflow.

Configuration example:

```toml
[module]
  [[module.imports]]
    path = "github.com/CaiJimmy/hugo-theme-stack/v3"
```

Implications:
- A local `themes/` directory may not exist.
- Theme files are typically overridden under `layouts/` instead of editing vendored theme files.
- AI must not assume that theme files are present locally unless confirmed.

---

# Directory Structure

Important directories:

```text
repo root
├─ content/
├─ data/
├─ layouts/
├─ assets/
├─ static/
├─ scripts/   (if present)
└─ docs/
```

Important note for Stack theme overrides:
- This project may use both `layouts/_default/` and Stack-style underscore partial paths such as `layouts/_partials/`.
- Do not assume that all theme partial overrides live under `layouts/partials/`.

---

# Post Structure

Each blog post is stored as:

```text
content/posts/<POST_ID>/index.md
```

Example:

```text
content/posts/6256/index.md
```

The post ID corresponds to the original FC2 blog entry number.

---

# URL Structure

New URL format:

```text
/posts/<POST_ID>/
```

Example:

```text
/posts/6256/
```

Old FC2 URL format:

```text
/blog-entry-6256.html
```

Redirect rules convert the old format to the new format.

---

# Migration Source

Original blog platform: FC2 Blog  
Export source file: `kiam.txt`

This file is converted using custom scripts.

---

# Migration Scripts

Scripts used for migration and maintenance:
- `fc2_export_to_hugo.py` — convert FC2 export data to Hugo posts
- `extract_comments.py` — extract comments from FC2 export and generate comment data
- `rebuild_archives.py` — generate archive data and archive pages

These scripts are run manually from the repository root.

---

# Archives System

Archive pages are generated automatically using a script.

Output files:
- `data/archives/months.json`
- `content/archives/YYYY/_index.md`
- `content/archives/YYYY/MM/_index.md`

Archives are generated deterministically by `rebuild_archives.py`.

---

# Comment System

Comments are imported from the FC2 export.

Workflow:

```text
FC2 export
↓
extract_comments.py
↓
comment data generated
↓
Hugo templates display comments
```

Latest comments page exists and works locally.

---

# Theme Customization

Theme used: `hugo-theme-stack`

The theme is customized using:
- custom CSS
- layout overrides
- partial templates

Some default theme behaviors are overridden.

Important current knowledge:
- The Stack theme footer source in the current upstream theme is under `layouts/_partials/footer/`.
- `footer/custom.html` is an optional hook for extra scripts/content, not the footer body itself.
- In this project, some custom templates call `{{ partial "footer/footer" . }}` manually, so footer visibility may depend on the individual layout template.

---

# Custom CSS

Custom CSS is used to reproduce the visual style of the original FC2 blog.

Examples:
- blockquote styling
- typography adjustments
- card layout spacing
- responsive layout tweaks
- footer appearance overrides when needed

---

# Additional Features

The site includes:
- Prism.js syntax highlighting
- Flickr embed support
- Google Maps embedding support
- custom archive pages
- redirect rules for legacy URLs

---

# Deployment

Deployment pipeline:

```text
GitHub repository
↓
Cloudflare Pages build
↓
Public site
```

Build tool: Hugo

---

# Local Development

Local preview command:

```bash
hugo server --disableFastRender
```

This runs a local preview server.

Note that some features may not work locally if they depend on external services.

---

# Important Design Goals

The project prioritizes:
- deterministic site generation
- stable URLs
- compatibility with old FC2 links
- minimal reliance on external services
- long-term maintainability

---

# AI Usage Instructions

When assisting with this project:
1. Always follow the architecture described in this file.
2. Avoid suggesting unrelated frameworks.
3. Prefer solutions compatible with Hugo and Cloudflare Pages.
4. Maintain compatibility with the existing URL structure.
5. Before suggesting theme file edits, confirm whether the theme file is a Hugo Module source file or a local override.

---

# Maintenance Rule

When a major change is made to the system architecture, this file should be updated accordingly.
The AI may generate update text, but the repository owner commits the changes manually.
