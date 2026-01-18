# 01. 環境構築・初期設定

**Status**: TODO
**Priority**: 最優先
**Estimated**: -

## 概要

開発環境の構築とプロジェクトの初期設定を行う。

## 関連する要件

- 技術スタック（REQUIREMENTS.md セクション3）

## Tasks

- [ ] Supabaseプロジェクトの作成・設定
- [ ] 環境変数の設定（`.env.local`）
  - [ ] NEXT_PUBLIC_SUPABASE_URL
  - [ ] NEXT_PUBLIC_SUPABASE_ANON_KEY
  - [ ] SUPABASE_SERVICE_ROLE_KEY
- [ ] Supabase Clientのセットアップ（`@supabase/supabase-js`）
- [ ] Cloudflare Pages デプロイ設定
- [ ] Cloudflare R2 バケット作成
- [ ] Stripe アカウント設定・API Key取得
- [ ] Gemini API Key取得・設定
- [ ] 共通の型定義ファイル作成（`src/types/`）

## 技術メモ

```bash
npm install @supabase/supabase-js
```

## 完了条件

- 全ての外部サービスとの接続が確認できる
- 環境変数が正しく設定されている
- `npm run dev`でエラーなく起動する
