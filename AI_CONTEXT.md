# AI Context — nikki-san (Cloudflare Pages + Hugo)

IMPORTANT
このファイルは **AI（ChatGPTなど）がこのプロジェクトを理解するための仕様書**です。
回答する前に必ずこのファイルの内容を前提にしてください。

AI assistants must read all files under / before answering.

---

# Project Overview

This project is a **static blog migrated from FC2 Blog**.

Platform stack:

* Hugo static site generator
* Hugo theme: **Stack**
* Hosted on **Cloudflare Pages**
* Source repository: GitHub
* Deployment: automatic from GitHub

Primary public URL:

https://nikki-san.pages.dev/

---

# Repository

GitHub repository:

https://github.com/65edh5ih/nikki-san

The site is built automatically by Cloudflare Pages when the repository is updated.

---

# Directory Structure

Important directories:

repo root

content/
posts/ <ID>/
index.md

data/
archives/
months.json

layouts/

static/

scripts/

docs/
AI_CONTEXT.md

---

# Post Structure

Each blog post is stored as:

content/posts/<POST_ID>/index.md

Example:

content/posts/6256/index.md

The post ID corresponds to the original FC2 blog entry number.

---

# URL Structure

New URL format:

/posts/<POST_ID>/

Example:

/posts/6256/

Old FC2 URL format:

/blog-entry-6256.html

Redirect rules convert the old format to the new format.

---

# Migration Source

Original blog platform:

FC2 Blog

Export source file:

kiam.txt

This file is converted using a custom script.

---

# Migration Scripts

Scripts used for migration and maintenance:

fc2_export_to_hugo.py
Convert FC2 export data to Hugo posts.

extract_comments.py
Extract comments from FC2 export and generate comment data.

rebuild_archives.py
Generate archive data and archive pages.

These scripts are run manually from the repository root.

---

# Archives System

Archive pages are generated automatically using a script.

Output files:

data/archives/months.json

content/archives/YYYY/_index.md

content/archives/YYYY/MM/_index.md

Archives are generated deterministically by `rebuild_archives.py`.

---

# Comment System

Comments are imported from the FC2 export.

Workflow:

FC2 export
↓
extract_comments.py
↓
comment data generated
↓
Hugo templates display comments

Latest comments page exists and works locally.

---

# Theme

Hugo theme used:

hugo-theme-stack

The theme is customized using:

* custom CSS
* layout overrides
* partial templates

Some default theme behaviors are overridden.

---

# Custom CSS

Custom CSS is used to reproduce the visual style of the original FC2 blog.

Examples:

* blockquote styling
* typography adjustments
* card layout spacing
* responsive layout tweaks

---

# Additional Features

The site includes:

Prism.js syntax highlighting
Flickr embed support
Google Maps embedding support
Custom archive pages
Redirect rules for legacy URLs

---

# Deployment

Deployment pipeline:

GitHub repository
↓
Cloudflare Pages build
↓
Public site

Build tool:

Hugo

---

# Local Development

Local preview command:

hugo server --disableFastRender

This runs a local preview server.

Note that some features may not work locally if they depend on external services.

---

# Important Design Goals

The project prioritizes:

* deterministic site generation
* stable URLs
* compatibility with old FC2 links
* minimal reliance on external services
* long-term maintainability

---

# AI Usage Instructions

When assisting with this project:

1. Always follow the architecture described in this file.
2. Avoid suggesting unrelated frameworks.
3. Prefer solutions compatible with Hugo and Cloudflare Pages.
4. Maintain compatibility with existing URL structure.

---

# Maintenance Rule

When a major change is made to the system architecture,
this file should be updated accordingly.

The AI may generate update text, but the repository owner
commits the changes manually.

---
