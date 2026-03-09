# Known Issues — nikki-san

このファイルは、現行運用で再発しやすいポイントを記録します。

## 1. 生成物の手修正が上書きされる

対象:
- `content/archives/**`
- `data/archives/months.json`
- `data/recent_comments.json`

理由:
- `rebuild_archives.py` / `extract_comments.py` 実行で再生成されるため。

対処:
- 原因をスクリプト側または入力データ側で修正する。

## 2. コメント件数・最新コメントの不整合

症状:
- 投稿ページのコメント表示とサイドバー最新コメントが一致しない。

確認:
- `comments/post-<id>.json`
- `data/recent_comments.json`
- `extract_comments.py` 実行結果

## 3. アーカイブ欠落

症状:
- 年/月アーカイブが欠ける、または件数不一致。

確認:
- 投稿front matterの日付
- `python3 ./rebuild_archives.py --verbose`

## 4. 旧FC2リンク遷移不良

症状:
- `/blog-entry-XXXX.html` から新URLへ遷移しない。

確認:
- `static/_redirects`
- Cloudflare Pages のデプロイ反映状態

## 5. エクスポート/インポート時の上書きミス

症状:
- `import_posts.py` で既存記事を意図せず上書き。

対処:
- まず `--no-overwrite` を使用して安全確認する。
