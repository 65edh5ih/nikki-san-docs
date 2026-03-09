# Repository Map — nikki-san

このドキュメントは、現行リポジトリ構成の要点をまとめたものです。

## Root (主要ファイル)

- `hugo.toml` — Hugoメイン設定
- `go.mod`, `go.sum` — Hugo module依存
- `fc2_export_to_hugo.py`
- `extract_comments.py`
- `rebuild_archives.py`
- `export_posts.py`
- `import_posts.py`

## content/

- `content/posts/<POST_ID>/index.md` — 記事
- `content/archives/` — 年/月アーカイブページ（再生成対象）

## comments/

- `comments/post-<POST_ID>.json` — 記事ごとのコメントデータ

## data/

- `data/archives/months.json` — アーカイブ一覧メタ
- `data/recent_comments.json` — 最新コメント一覧

## layouts/

Stackテーマのオーバーライドテンプレート。

- `_default/`
- `partials/`
- `section/`
- `page/`
- `shortcodes/`
- `m/`（軽量版トップ用）

## assets/

Hugo Pipes経由で処理されるファイル。

- `assets/scss/`
- `assets/js/`
- `assets/icons/`
- `assets/img/`

## static/

そのまま配信する静的ファイル。

- `static/_redirects`
- `static/css/prism.css`
- `static/js/prism.js`
- `static/js/mobile-redirect.js`
- `static/robots.txt`

## AI documentation (repo root)

AI仕様書一式。

- `AI_CONTEXT.md`
- `AI_DEBUG_GUIDE.md`
- `AI_PROMPT_TEMPLATE.md`
- `AI_TASK_HISTORY.md`
- `ARCHITECTURE.md`
- `KNOWN_ISSUES.md`
- `REPO_MAP.md`
- `SCRIPTS.md`

## public/

ローカルビルド成果物（追跡されるケースあり）。
