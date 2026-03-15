# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリで作業する際のガイドです。

## プロジェクト概要

Hugo + PaperModテーマで構築された日本語の個人ブログ（「Culthouse Liminal」）。GitHub Actionsを使ってGitHub Pagesにデプロイされる。

## コマンド

- `hugo server -D` — ローカル開発サーバー（下書き記事も表示）
- `hugo --minify` — 本番ビルド（`public/` に出力）
- `hugo new posts/<slug>.md` — アーキタイプテンプレートから新規記事を作成

Hugo拡張版（extended edition）が必要。npm/yarn等の依存関係はなし。

## アーキテクチャ

- **hugo.toml** — サイト設定（ベースURL、テーマ、メニュー、言語）
- **content/posts/** — TOML形式のフロントマター（`+++`）を持つMarkdownブログ記事
- **themes/PaperMod/** — テーマ（`adityatelange/hugo-PaperMod` のgitサブモジュール）。ここのファイルは直接編集せず、プロジェクトルートの `layouts/` や `assets/` でオーバーライドすること
- **archetypes/default.md** — `hugo new` 用の記事テンプレート
- **public/** — 生成された出力（gitignore対象）

## デプロイ

`main` ブランチへのプッシュで `.github/workflows/hugo.yml` が起動し、`hugo --minify` でビルド後、GitHub Pagesにデプロイされる。CI時にテーマのサブモジュールが再帰的にクローンされる。

## コンテンツの規約

- 言語: 日本語（`languageCode = "ja"`）
- フロントマター形式: TOML（`+++` 区切り）
- 新規記事はデフォルトで `draft = true`。公開するには `draft = false` に変更する
