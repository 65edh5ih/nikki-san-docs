# AI Prompt Template — nikki-san

This file contains a template prompt used when starting a new AI session.

Its purpose is to ensure that AI assistants understand the project context before answering.

---

# Usage

When starting a new AI conversation, paste the template below.

---

# Prompt Template

You are assisting with the **nikki-san blog project**.

Before answering, read the following documentation:

AI_CONTEXT
docs/AI_CONTEXT.md

ARCHITECTURE
docs/ARCHITECTURE.md

DEBUG RULES
docs/AI_DEBUG_GUIDE.md

SCRIPTS
docs/SCRIPTS.md

REPOSITORY MAP
docs/REPO_MAP.md

KNOWN ISSUES
docs/KNOWN_ISSUES.md

TASK HISTORY
docs/AI_TASK_HISTORY.md

These documents describe the system architecture and debugging rules.

You must follow the debugging rules defined in `AI_DEBUG_GUIDE.md`.

In particular:

Do not guess.
Request files or command outputs when necessary.
Avoid generic advice unrelated to Hugo or Cloudflare Pages.

---

# Project Summary

This project is a static blog migrated from FC2 Blog.

Stack:

Hugo
Hugo theme Stack
Cloudflare Pages
GitHub repository
Python migration scripts

Post structure:

content/posts/<POST_ID>/index.md

URL structure:

/posts/<POST_ID>/

Legacy URLs:

/blog-entry-XXXX.html

Redirect rules preserve compatibility.

---

# When Debugging

Before proposing a solution, confirm:

relevant files
error messages
command outputs
directory structure

Avoid speculative debugging.

---

# Task

Now help with the following task:

[Describe the current problem here]

---

# Example

Task:

Hugo build fails with a JSON template rendering error.

Error message:

[Paste error message]

Relevant files:

[Paste template file]

---

# Goal

The goal is to obtain **accurate and architecture-aware**