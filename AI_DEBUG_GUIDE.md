# AI Debug Guide — nikki-san

This document defines **rules for AI when debugging or proposing changes** in this project.

The goal is to **avoid hallucinations and speculative answers**.

---

# Rule 1 — Evidence First

AI must not guess.

Before proposing a fix, the AI must ask for:

* file contents
* error messages
* command outputs
* configuration files

Example:

Incorrect approach:

"Maybe the problem is..."

Correct approach:

"Please show the contents of the following file."

---

# Rule 2 — No Random Configuration Suggestions

AI must not suggest configuration changes without verifying:

* the exact file
* the current configuration
* the version of the tool involved

Example tools requiring verification:

Hugo
Cloudflare Pages
Hugo theme Stack

---

# Rule 3 — Do Not Assume File Locations

Before referencing files, confirm the directory structure.

Ask for:

repository tree

Example command:

```
tree -L 3
```

---

# Rule 4 — Avoid Generic Web Advice

Do not propose solutions intended for:

WordPress
Next.js
generic Node.js sites

This project uses **Hugo static generation**.

---

# Rule 5 — Prefer Minimal Changes

When proposing a fix:

prefer the smallest possible modification.

Avoid:

large refactoring
changing unrelated components

---

# Rule 6 — Preserve URL Stability

Do not propose changes that alter the URL structure:

/posts/<ID>/

unless explicitly requested.

Existing links must remain valid.

---

# Rule 7 — Scripts Are Authoritative

Migration and archive scripts define the system behavior.

Files:

fc2_export_to_hugo.py
extract_comments.py
rebuild_archives.py

Before modifying Hugo templates, verify whether the issue originates in these scripts.

---

# Rule 8 — Deterministic Output

The system relies on deterministic generation.

AI must avoid solutions that introduce:

non-deterministic builds
external runtime dependencies

---

# Rule 9 — Ask Before Editing Theme Behavior

The Hugo Stack theme may have custom overrides.

Before proposing theme changes, confirm:

layouts/ overrides
custom CSS

---

# Rule 10 — When Unsure

If the AI lacks sufficient information:

ask for more data instead of guessing.

Example:

Please show the relevant template file.

---

# Goal

Following these rules ensures:

reliable debugging
minimal hallucination
safe architecture evolution