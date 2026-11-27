# ZERO BASE SENDAI ホームページ

ジム「ZERO BASE SENDAI」の1ページ構成の静的サイト。2026-11-19納品版をもとにしている。

## 構成
- `site/index.html`：ページ本体。文言はすべてこの1ファイルにある。各セクションの先頭に `▼▼▼ <セクション名>` のコメント目印がある
- `site/assets/`：写真・ロゴ（webp）
- `site/firebase.json` / `site/.firebaserc`：Firebase Hosting の設定。公開ディレクトリは `site/` 自体（`"public": "."`）
- `EDIT_GUIDE.html`（編集ガイド。Macのunzipが日本語ファイル名で失敗するため英語名にしている）：納品時に付いていた、オーナー向けの編集ガイド

## 公開
- URL: https://zero-base-sendai.web.app （Firebaseプロジェクト: `zero-base-sendai`）
- **自動公開（GitHub Actions）設定済み**（2026-11-27、初回の手動実行で成功を確認）
  - `.github/workflows/deploy.yml`：`main` の `site/` が変わると、1〜2分で本番に公開される
  - 認証はシークレット `FIREBASE_SERVICE_ACCOUNT_ZERO_BASE_SENDAI`（Firebase Hosting 管理者権限のサービスアカウント）
  - 手動で再公開したいときは REST で dispatch する（このセッション環境では GraphQL が使えないため `gh workflow run` は不可）:
    `gh api -X POST repos/ssassaki1204-lgtm/zerobase-sendai-site/actions/workflows/deploy.yml/dispatches -f ref=main`
  - 結果の確認: `gh api repos/ssassaki1204-lgtm/zerobase-sendai-site/actions/runs --jq '.workflow_runs[0]|[.status,.conclusion]'`
- 編集の流れ：このリポジトリの `main` を編集して push する → Actions の成功を確認する → オーナーに「反映済み」と伝える（オーナーの作業は不要。スマホから依頼できる）
- 予備の公開コマンド（Actions が使えないときだけ。オーナーのMacで、どこからでも実行できる。GitHubから最新の `main` を取ってきて公開する）:
  ```
  cd /tmp && rm -rf zerobase-sendai-site-main zb.zip && curl -fsSL -o zb.zip https://github.com/ssassaki1204-lgtm/zerobase-sendai-site/archive/refs/heads/main.zip && unzip -q zb.zip && cd zerobase-sendai-site-main/site && firebase deploy --only hosting --project zero-base-sendai
  ```
  - このコマンドはリポジトリが Public であることが前提。Private にした場合は使えない
  - オーナーのMacには firebase-tools がインストール済みで、ログインも済んでいる（2026-11-26時点）
- `firebase init` は実行しないこと。`firebase.json` が上書きされる
- HTMLはブラウザに1時間キャッシュされる。公開直後の確認は `?1` を付けたURLで行う

## 編集時の注意
- 同じ情報がページ内の複数箇所にある。変更するときは全箇所をまとめて直す（`EDIT_GUIDE.html` の4章を参照）
  - オープン時期（`12月下旬` / `2026.12`）、公式LINE（`lin.ee/ShvPHxf`）、Instagram（`zero.base.sendai`）、メール（`info@zerobasegym.com`）、住所（`萩野町`）
  - ジム名・住所・オープン時期が変わったら、`<title>`、`description`、`application/ld+json` も直す
- Googleマップの埋め込みは店舗の cid を使う: `https://www.google.com/maps?cid=5868064482876122627&output=embed`
  - 「Google Mapで開く」ボタンのリンク先: `https://maps.app.goo.gl/Eqc7rrnPTwpS5SVy7`
- 地図には意図的に `filter:grayscale(1)` がかけてある（`.map` クラス）
- 変更したら、PC幅（1280px）とスマホ幅（iPhone）の両方で表示を確認する。セクションはスクロールで現れるアニメーション付き（`[data-rv]` → `.in`）

## オーナーについて
- 開発者ではない。説明は日本語で、手順はコピペできるコマンド単位で書く
