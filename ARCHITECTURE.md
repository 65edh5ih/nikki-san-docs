# Architecture — nikki-san

## 1. System

このシステムは Hugo ベースの静的ブログです。データ源は FC2 由来で、GitHub 管理 + Cloudflare Pages デプロイで運用します。

フロー:

1. FC2データ取り込み / 変換
2. `content/posts/<ID>/index.md` を正本として管理
3. 補助データ（comments / archives）をスクリプト生成
4. Hugo build
5. Cloudflare Pages 配信

## 2. Content Model

- Posts: `content/posts/<POST_ID>/index.md`
- Archives pages: `content/archives/YYYY/MM/_index.md` など
- Comments data: `comments/post-<POST_ID>.json`
- Data files:
  - `data/archives/months.json`
  - `data/recent_comments.json`

`content/archives/*` は基本的に `rebuild_archives.py` の生成対象です。

## 3. Script Layer

### fc2_export_to_hugo.py
FC2エクスポートテキストを解析し、Hugo記事を生成。

### extract_comments.py
記事Markdown内の「## コメント」セクションを抽出し、
- `comments/post-<id>.json`
- `data/recent_comments.json`
を更新。必要に応じて記事本文からコメント節を除去。

### rebuild_archives.py
`content/posts/**/index.md` の front matter 日付を走査し、
- `data/archives/months.json`
- `content/archives/` ツリー
を再構築。`--dry-run`, `--verbose` あり。

### export_posts.py / import_posts.py
AI連携・バックアップ用途のテキスト形式エクスポート/インポート。

- export: `export/` 配下に `all.txt`, `by-year`, `by-month`, `by-size`, `manifest.json`
- import: `<<<HUGO_POST:ID>>>` 区切り形式から `content/posts` 復元

## 4. Theme / Rendering Layer

- Theme module: Stack v3
- Override: `layouts/` 配下
- Styling:
  - `assets/scss/*.scss`
  - `static/css/prism.css`
- Scripts:
  - `static/js/prism.js`
  - `assets/js/comments.js`, `assets/js/comments-count.js`

## 5. Deployment Layer

- GitHub push
- Cloudflare Pages build
- 公開 (`https://nikki-san.com/`)

## 6. Key Constraints

- URL安定性（`/posts/<ID>/`）
- 旧FC2リンク互換（リダイレクト）
- 生成処理の再現性（deterministic）
- テーマ改変は原則 `layouts/` オーバーライドで実施
