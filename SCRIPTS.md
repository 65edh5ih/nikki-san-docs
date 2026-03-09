# Scripts — nikki-san

このドキュメントは、現行スクリプトの用途と実行順を定義します。

## Available Scripts (repo root)

1. `fc2_export_to_hugo.py`
2. `extract_comments.py`
3. `rebuild_archives.py`
4. `export_posts.py`
5. `import_posts.py`

---

## 1) fc2_export_to_hugo.py

目的: FC2 exportテキストから Hugo 記事を生成。

主な出力:
- `content/posts/<POST_ID>/index.md`

備考:
- FC2由来IDを維持
- front matter + 本文変換

---

## 2) extract_comments.py

目的: 記事Markdownのコメントセクションを抽出し、JSON化。

実行例:

```bash
python3 ./extract_comments.py content/posts comments
```

主な出力:
- `comments/post-<POST_ID>.json`
- `data/recent_comments.json`

副作用:
- 記事内コメントブロックを本文から除去して更新する場合あり

---

## 3) rebuild_archives.py

目的: アーカイブデータ/ページの再構築。

実行例:

```bash
python3 ./rebuild_archives.py
python3 ./rebuild_archives.py --dry-run --verbose
```

主な出力:
- `data/archives/months.json`
- `content/archives/_index.md`
- `content/archives/YYYY/_index.md`
- `content/archives/YYYY/MM/_index.md`

---

## 4) export_posts.py

目的: `content/posts` を AI作業・移送向けテキストにエクスポート。

主な出力:
- `export/all.txt`
- `export/by-year/*.txt`
- `export/by-month/*.txt`（必要時 `.partNN` 分割）
- `export/by-size/chunk-XXXX.txt`
- `export/manifest.json`

仕様:
- エントリは `<<<HUGO_POST:ID>>>` マーカーで区切る
- 5MB上限を基準に分割（境界は投稿単位）

---

## 5) import_posts.py

目的: エクスポートテキストから `content/posts` を再生成。

実行例:

```bash
python3 ./import_posts.py export/all.txt
python3 ./import_posts.py export/by-month --no-overwrite
```

オプション:
- `--out <DIR>`（デフォルト `content/posts`）
- `--no-overwrite`

入力:
- 単一 `.txt`
- `.txt` を含むディレクトリ（再帰）

---

## Recommended Order

FC2データからサイト更新する一般順序:

1. `fc2_export_to_hugo.py`
2. `extract_comments.py`
3. `rebuild_archives.py`
4. （必要に応じて）`hugo` / `hugo server`

AI連携用バックアップ/復元:

- エクスポート: `export_posts.py`
- 復元: `import_posts.py`

---

## Determinism

これらスクリプトは、同じ入力に対して安定した出力を返す設計を優先します。差分が大きい場合は入力ファイルや日付/front matterを先に確認してください。
