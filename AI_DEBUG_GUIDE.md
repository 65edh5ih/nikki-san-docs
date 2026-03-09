# AI Debug Guide — nikki-san

## 目的

Hugo + Stack + Cloudflare Pages 前提で、推測を減らし、最小変更で原因を特定する。

## ルール

1. **Evidence first**
   - エラー文、対象ファイル、実行コマンド結果を先に確認。
2. **構成前提を守る**
   - Node/Next.js/WordPress向けの一般論を持ち込まない。
3. **URL安定性を壊さない**
   - `/posts/<ID>/` と旧FC2互換を維持。
4. **生成物を直接修正しない**
   - `content/archives/*`, `data/archives/months.json`, `data/recent_comments.json` は原則スクリプト再生成で直す。
5. **スクリプト起点で原因を切り分ける**
   - アーカイブ不整合: `rebuild_archives.py`
   - コメント不整合: `extract_comments.py`
6. **テーマ改修は override 優先**
   - `layouts/` と `assets/` の範囲で最小修正。

## 推奨確認コマンド

```bash
git status --short
python3 ./rebuild_archives.py --dry-run --verbose
python3 ./extract_comments.py content/posts comments
hugo
```

## よくある論点

- Prism表示崩れ: `static/js/prism.js`, `static/css/prism.css` 読み込みを確認
- リダイレクト不整合: `static/_redirects` を確認
- Markdown内HTML不表示: `hugo.toml` の `markup.goldmark.renderer.unsafe` を確認
