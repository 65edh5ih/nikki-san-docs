# Scripts — nikki-san

This document describes the purpose and behavior of the Python scripts used in the nikki-san blog system.

These scripts are responsible for converting and generating data used by Hugo.

All scripts are executed manually from the repository root.

---

# Script Overview

The project includes three main scripts:

fc2_export_to_hugo.py
extract_comments.py
rebuild_archives.py

These scripts transform the original FC2 blog export into a structure usable by Hugo.

---

# fc2_export_to_hugo.py

Purpose:

Convert FC2 export data into Hugo-compatible posts.

Input:

FC2 export file

Example:

~/kiam.txt

Output:

Hugo post directories

content/posts/<POST_ID>/index.md

Example:

content/posts/6256/index.md

Responsibilities:

* parse FC2 export format
* extract post metadata
* convert article body to Markdown
* maintain original FC2 entry IDs
* preserve chronological order

Typical command:

```id="8o6p1n"
python3 ./fc2_export_to_hugo.py ~/kiam.txt content/posts
```

Example output:

written=6256
skipped=1

Where:

written = number of posts generated
skipped = entries ignored due to parsing issues

---

# extract_comments.py

Purpose:

Extract comments from the FC2 export and generate structured comment data.

Input:

Hugo post directory

Example:

content/posts/

Output:

comment data used by Hugo templates.

The script associates comments with post IDs.

Responsibilities:

* parse comment blocks
* attach comments to the correct post
* generate data used by the comment display system

Typical command:

```id="h6jv9b"
python3 ./extract_comments.py content/posts comments
```

---

# rebuild_archives.py

Purpose:

Generate archive pages and metadata for the site.

Input:

post metadata from content/posts

Output:

data/archives/months.json

content/archives/YYYY/_index.md

content/archives/YYYY/MM/_index.md

Responsibilities:

* scan all posts
* group posts by year and month
* generate archive pages
* ensure deterministic output

Typical command:

```id="9i5px2"
python3 ./rebuild_archives.py
```

Optional flags may include:

--dry-run
--verbose

---

# Script Execution Order

Typical workflow after importing or modifying posts:

1. convert posts

fc2_export_to_hugo.py

2. extract comments

extract_comments.py

3. rebuild archive pages

rebuild_archives.py

---

# Deterministic Design

All scripts are designed to produce deterministic output.

This means:

running the scripts multiple times should produce identical results.

This property is important for stable Hugo builds and predictable Git diffs.

---

# Error Handling

If a script reports errors:

1. inspect the input data
2. check the affected post ID
3. review the parsing logic

Common causes include:

unexpected FC2 export format
invalid metadata fields
malformed HTML

---

# Debugging Scripts

When debugging scripts, the AI should request:

example input data
the generated output file
error messages
the relevant section of the script

Avoid modifying parsing logic without inspecting the original export data.

---

# Maintenance Rules

When a script changes behavior:

update this document.

Changes that affect site structure must also update:

AI_CONTEXT.md
ARCHITECTURE.md