# ZERO BASE SENDAI ホームページ

ジム「ZERO BASE SENDAI」の1ページ構成の静的サイト。2026-11-19納品版をもとにしている。

## 構成
- `site/index.html`：ページ本体。文言はすべてこの1ファイルにある。各セクションの先頭に `▼▼▼ <セクション名>` のコメント目印がある
- `site/assets/`：写真・ロゴ（webp）
- `site/firebase.json` / `site/.firebaserc`：Firebase Hosting の設定。公開ディレクトリは `site/` 自体（`"public": "."`）
- `編集ガイド.html`：納品時に付いていた、オーナー向けの編集ガイド

## 公開
- URL: https://zero-base-sendai.web.app （Firebaseプロジェクト: `zero-base-sendai`）
- 公開コマンド（`site/` で実行）: `firebase deploy --only hosting --project zero-base-sendai`
- `firebase init` は実行しないこと。`firebase.json` が上書きされる
- HTMLはブラウザに1時間キャッシュされる。公開直後の確認は `?1` を付けたURLで行う

## 編集時の注意
- 同じ情報がページ内の複数箇所にある。変更するときは全箇所をまとめて直す（`編集ガイド.html` の4章を参照）
  - オープン時期（`12月下旬` / `2026.12`）、公式LINE（`lin.ee/ShvPHxf`）、Instagram（`zero.base.sendai`）、メール（`info@zerobasegym.com`）、住所（`萩野町`）
  - ジム名・住所・オープン時期が変わったら、`<title>`、`description`、`application/ld+json` も直す
- Googleマップの埋め込みは店舗の cid を使う: `https://www.google.com/maps?cid=5868064482876122627&output=embed`
  - 「Google Mapで開く」ボタンのリンク先: `https://maps.app.goo.gl/Eqc7rrnPTwpS5SVy7`
- 地図には意図的に `filter:grayscale(1)` がかけてある（`.map` クラス）
- 変更したら、PC幅（1280px）とスマホ幅（iPhone）の両方で表示を確認する。セクションはスクロールで現れるアニメーション付き（`[data-rv]` → `.in`）

## オーナーについて
- 開発者ではない。説明は日本語で、手順はコピペできるコマンド単位で書く
