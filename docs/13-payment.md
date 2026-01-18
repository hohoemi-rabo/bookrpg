# 13. 決済機能（Stripe）

**Status**: TODO
**Priority**: 高
**Depends on**: 11-audio-player

## 概要

Stripe Checkoutを使用した有料章の購入機能。

## 関連する要件

- 5. ビジネスモデル（REQUIREMENTS.md）
- 4.4.5 生成失敗時の対応（REQUIREMENTS.md）

## Tasks

### Stripe設定
- [ ] Stripe Checkoutの設定
- [ ] 商品（残り章すべて ¥200）の登録
- [ ] Webhook設定

### 購入フロー
- [ ] 購入ボタン表示（無料章再生後）
- [ ] 購入確認画面
- [ ] Stripe Checkoutへのリダイレクト
- [ ] 購入完了後のコールバック処理
- [ ] 購入完了画面

### Webhook処理
- [ ] payment_intent.succeeded の処理
- [ ] purchasesテーブルへの記録
- [ ] chaptersテーブルのis_purchased更新
- [ ] 署名検証

### 購入状態管理
- [ ] 購入済みかどうかの判定
- [ ] 購入済み章へのアクセス制御

### 返金対応
- [ ] 生成失敗時の返金フロー設計
- [ ] 返金処理の実装（管理画面から）

### API
- [ ] POST /api/purchases（購入処理開始）
- [ ] POST /api/purchases/webhook（Stripe Webhook）

## 料金体系

| プラン           | 内容             | 価格 |
| ---------------- | ---------------- | ---- |
| 無料             | 1冊につき1章のみ | ¥0   |
| 有料（買い切り） | 残りの章すべて   | ¥200 |

## ファイル構成

```
src/
├── app/
│   ├── (protected)/
│   │   └── purchase/
│   │       ├── [questId]/
│   │       │   └── page.tsx
│   │       └── complete/
│   │           └── page.tsx
│   └── api/
│       └── purchases/
│           ├── route.ts
│           └── webhook/
│               └── route.ts
└── lib/
    └── stripe/
        └── client.ts
```

## 完了条件

- Stripe Checkoutで購入できる
- 購入完了後に全章がアンロックされる
- Webhookが正しく処理される
- 購入履歴が記録される
