# AI Task History — nikki-san

This document records **major tasks performed with AI assistance**.

Its purpose is to provide context for future AI sessions and avoid repeating the same discussions.

Only significant architectural or system-level changes should be recorded here.

---

# 2026 — FC2 Blog Migration

## Overview

The nikki-san blog was migrated from FC2 Blog to a static site architecture.

The new system uses:

Hugo
Cloudflare Pages
GitHub repository

The goal was to preserve all historical content while improving long-term maintainability.

---

## Post Migration

Original FC2 export data:

kiam.txt

Posts were converted using a custom script:

fc2_export_to_hugo.py

Output structure:

content/posts/<POST_ID>/index.md

The POST_ID corresponds to the original FC2 blog entry number.

---

## Comment Migration

FC2 comments were extracted and converted into structured comment data.

Script used:

extract_comments.py

Comments are associated with posts using the original FC2 entry ID.

---

## Archive System

Archive pages were implemented using a script.

Script:

rebuild_archives.py

Generated files include:

data/archives/months.json

content/archives/YYYY/_index.md

content/archives/YYYY/MM/_index.md

Archives are generated deterministically.

---

## Hugo Theme

Theme used:

hugo-theme-stack

The theme has been customized to reproduce visual aspects of the original FC2 blog.

Customizations include:

CSS adjustments
layout overrides
typography changes

---

## Visual Adjustments

Several adjustments were made to match the original FC2 design.

Examples include:

blockquote styling
spacing adjustments
card layout tuning

These changes are implemented through custom CSS and theme overrides.

---

## Syntax Highlighting

Prism.js was added for code block highlighting.

Files are placed under:

static/js/
static/css/

---

## Additional Embeds

The blog supports embedded content including:

Flickr images
Google Maps

These are integrated directly in Markdown content.

---

## Redirects

Legacy FC2 URLs follow this pattern:

/blog-entry-XXXX.html

The Hugo site uses:

/posts/<POST_ID>/

Redirect rules ensure that old links remain valid.

---

# Documentation System

To improve AI collaboration, the repository includes documentation files under:

docs/

These include:

AI_CONTEXT.md
ARCHITECTURE.md
AI_DEBUG_GUIDE.md
SCRIPTS.md
REPO_MAP.md
KNOWN_ISSUES.md
AI_TASK_HISTORY.md

These documents ensure that future AI sessions understand the system architecture.

---

# Maintenance Rule

When a major change is introduced, append a new section with:

date
task summary
files affected
design decisions

This helps future debugging and AI-assisted development.