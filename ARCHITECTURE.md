# Architecture — nikki-san

This document describes the **technical architecture of the nikki-san blog system**.

It complements `AI_CONTEXT.md` by explaining **how components interact**.

---

# System Overview

The system is a **static blog platform built using Hugo** and deployed via **Cloudflare Pages**.

Architecture flow:

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

---

# Source Data

Original platform:

FC2 Blog

Export source file:

kiam.txt

This file contains:

* blog entries
* metadata
* comments

---

# Migration Layer

Migration is performed using custom Python scripts.

## fc2_export_to_hugo.py

Purpose:

Convert FC2 export data into Hugo-compatible content.

Output structure:

content/posts/<POST_ID>/index.md

Responsibilities:

* parse FC2 export format
* extract post metadata
* convert body to Markdown
* maintain original post IDs

---

## extract_comments.py

Purpose:

Extract comments from the FC2 export.

Responsibilities:

* parse comment sections
* associate comments with post IDs
* generate comment data used by Hugo

The comment data is later rendered in templates.

---

# Content Layer

Hugo content directory:

content/posts/

Each post is structured as:

content/posts/<POST_ID>/index.md

Example:

content/posts/6256/index.md

Advantages of this structure:

* stable permalink
* easy asset management
* consistent mapping from FC2 entry ID

---

# Archive Generation

Archives are generated using a script.

Script:

rebuild_archives.py

Generated files:

data/archives/months.json

content/archives/YYYY/_index.md

content/archives/YYYY/MM/_index.md

The generation process is deterministic.

The script reads post metadata and builds:

* year archives
* month archives

---

# Theme Layer

Theme used:

hugo-theme-stack

Theme customization includes:

* layout overrides
* CSS customization
* additional partial templates

Overrides may exist under:

layouts/

Common override locations:

layouts/_default/
layouts/partials/

---

# Styling Layer

Custom CSS is applied to reproduce the original FC2 blog visual style.

Typical modifications include:

* blockquote appearance
* typography adjustments
* card layout spacing
* responsive tweaks

Custom CSS may exist in:

assets/scss/
static/css/

---

# Rendering Layer

Hugo generates the final static site.

Command used locally:

hugo server --disableFastRender

Output directory:

public/

The static site includes:

* HTML
* CSS
* JS
* images

---

# Deployment Layer

Deployment pipeline:

GitHub repository
↓
Cloudflare Pages build
↓
public site

Cloudflare Pages automatically rebuilds the site when the repository changes.

---

# URL Compatibility

Legacy FC2 URLs:

/blog-entry-XXXX.html

New URLs:

/posts/<POST_ID>/

Redirect rules ensure compatibility with old links.

---

# Additional Components

The site includes additional features:

syntax highlighting (Prism.js)
Flickr embeds
Google Maps embeds

These features are integrated through Hugo templates or Markdown content.

---

# Design Principles

The architecture follows these principles:

deterministic generation
stable URL structure
minimal runtime dependencies
long-term maintainability

---

# When Updating Architecture

If the architecture changes significantly, update:

AI_CONTEXT.md
ARCHITECTURE.md

to reflect the new design.