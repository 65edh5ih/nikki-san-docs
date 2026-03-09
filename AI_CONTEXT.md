# AI Context — nikki-san

このファイルは、AIアシスタント向けのプロジェクト前提情報です。回答や修正提案の前に、リポジトリルートの関連ドキュメントを確認してください。

## Project Overview

`nikki-san` は FC2 Blog 由来のデータを Hugo で運用する静的ブログです。

- Static site generator: Hugo
- Theme: `github.com/CaiJimmy/hugo-theme-stack/v3`（Hugo Modules）
- Hosting: Cloudflare Pages
- Source control: GitHub

主要URL:

- Production: `https://nikki-san.com/`

## Core Repository Structure

主要ディレクトリ（実在）:

- `content/posts/<POST_ID>/index.md` — 記事本体
- `content/archives/` — 年/月アーカイブページ（生成物）
- `comments/post-<POST_ID>.json` — 記事ごとのコメントJSON
- `data/archives/months.json` — アーカイブメタデータ
- `data/recent_comments.json` — 最新コメントウィジェット用データ
- `layouts/` — テーマオーバーライド
- `assets/` — Hugo Pipes入力（SCSS/JS等）
- `static/` — そのまま配信される静的ファイル
- ルート直下 `*.md`（本ファイル群） — AI向け仕様書

## URL and Compatibility

- 現行記事URL: `/posts/<POST_ID>/`
- 旧FC2互換: `/blog-entry-XXXX.html`（`static/_redirects` で吸収）

URLの安定性は重要要件です。

## Data Pipeline (Current)

現在の運用で使われる主なスクリプト（リポジトリ直下）:

- `fc2_export_to_hugo.py` — FC2 exportテキストから Hugo 記事を生成
- `extract_comments.py` — 記事内コメントブロックを `comments/` JSON と `data/recent_comments.json` に反映
- `rebuild_archives.py` — `data/archives/months.json` と `content/archives/` を再生成
- `export_posts.py` — `content/posts` から AI/バックアップ向けテキスト分割エクスポートを作成
- `import_posts.py` — `export_posts.py` 形式のテキストを `content/posts` に再インポート

## Hugo Runtime Notes

- `hugo.toml` の `baseURL` は `https://nikki-san.com/`
- Goldmark は `unsafe = true`, `hardWraps = true`
- ホーム/ページのウィジェットに検索・アーカイブを使用
- コメント設定値（Turnstile site key, recent件数）を `params.comments` に保持

## Working Principles for AI

1. 推測ではなく、実ファイル確認を優先する。
2. Hugo + Stack + Cloudflare Pages 前提を崩さない。
3. 生成物（archives/data/comments）とソース（posts/layouts/scripts）を区別する。
4. 既存URL/IDベース構造（`<POST_ID>`）を維持する。

## Maintenance

アーキテクチャや運用スクリプトに変更があった場合は、ルート直下の仕様書を合わせて更新してください。
