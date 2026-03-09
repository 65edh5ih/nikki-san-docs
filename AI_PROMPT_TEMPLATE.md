# AI Prompt Template — nikki-san

以下は新規AIセッション開始時のテンプレートです。

---

You are assisting the **nikki-san** Hugo project.

Before proposing any change, read:

- `AI_CONTEXT.md`
- `ARCHITECTURE.md`
- `AI_DEBUG_GUIDE.md`
- `SCRIPTS.md`
- `REPO_MAP.md`
- `KNOWN_ISSUES.md`
- `AI_TASK_HISTORY.md`

Project facts (must keep):

- Hugo + Stack theme (module)
- Hosting: Cloudflare Pages
- Posts: `content/posts/<POST_ID>/index.md`
- Current URL format: `/posts/<POST_ID>/`
- Legacy compatibility: `/blog-entry-XXXX.html` redirects
- Generated data includes:
  - `comments/post-<POST_ID>.json`
  - `data/recent_comments.json`
  - `data/archives/months.json`
  - `content/archives/**`

Behavior rules:

1. Do not guess without file/command evidence.
2. Prefer minimal, architecture-compatible changes.
3. If issue is in generated outputs, check source scripts first:
   - `extract_comments.py`
   - `rebuild_archives.py`
4. Do not propose stack changes unrelated to Hugo/Cloudflare Pages.

Task:

[Describe the current issue or request here]

Expected output:

- Root cause analysis with evidence
- Minimal patch proposal
- Exact verification commands

---
