# 03. 認証機能（Google OAuth）

**Status**: TODO
**Priority**: 最優先
**Depends on**: 01-environment-setup, 02-database-design

## 概要

Supabase Authを使用したGoogle OAuth認証の実装。

## 関連する要件

- 4.1 認証機能（REQUIREMENTS.md）

## Tasks

- [ ] Supabase AuthでGoogle OAuth設定
- [ ] Google Cloud ConsoleでOAuth認証情報作成
- [ ] ログインページの作成（`/login`）
- [ ] ログインボタンコンポーネント作成
- [ ] 認証状態管理のContext/Provider作成
- [ ] 認証ミドルウェア作成（保護ルート用）
- [ ] ログアウト機能実装
- [ ] セッション管理（自動更新）
- [ ] 認証後のリダイレクト処理

## ファイル構成

```
src/
├── app/
│   ├── login/
│   │   └── page.tsx
│   └── auth/
│       └── callback/
│           └── route.ts
├── components/
│   └── auth/
│       ├── LoginButton.tsx
│       └── LogoutButton.tsx
├── contexts/
│   └── AuthContext.tsx
└── lib/
    └── supabase/
        ├── client.ts
        └── server.ts
```

## 完了条件

- Googleログイン/ログアウトが動作する
- 認証状態がアプリ全体で共有される
- 保護ルートへの未認証アクセスがリダイレクトされる
