# AI Task History — nikki-san

AI支援で実施した主要タスクの履歴。

## 2026-xx — AI仕様書の実態同期（現行リポジトリ反映）

### 背景

一部AI仕様書の説明が旧運用（スクリプト名・ディレクトリ前提）に寄っており、現行リポジトリ構成と差分があった。

### 更新内容

- `export_posts.py` / `import_posts.py` を公式運用スクリプトとして明記
- `comments/` と `data/recent_comments.json` の現行コメント導線を明記
- `rebuild_archives.py` の `--dry-run`, `--verbose` を追記
- `hugo.toml` の現行前提（baseURL・Goldmark・theme module）に合わせた説明へ更新
- 旧記述の「scripts/ ディレクトリ前提」を削除し、リポジトリ直下実行へ統一

### 影響

- AIセッションの初期前提ズレを低減
- デバッグ時の誤誘導（生成物直修正など）を抑制
