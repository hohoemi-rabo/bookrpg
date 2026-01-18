# 05. ランディングページ

**Status**: TODO
**Priority**: 高
**Depends on**: 03-authentication, 04-common-ui-components

## 概要

サービス紹介とログイン導線を持つランディングページの作成。

## 関連する要件

- 付録A: 画面一覧 - ランディングページ（REQUIREMENTS.md）

## Tasks

- [ ] ヒーローセクション（コンセプト表示）
  - 「その知識は、物語の中で『武器』になる」
- [ ] サービス説明セクション
  - 3ステップで説明（登録→生成→再生）
- [ ] 世界観紹介セクション（ファンタジー/SF/学園）
- [ ] CTAボタン（Google ログイン）
- [ ] フッター（利用規約等へのリンク）
- [ ] OGP/メタデータ設定
- [ ] アニメーション演出（任意）

## デザイン方針

- RPG風の雰囲気
- 「冒険が始まる」感を演出
- スマホファーストで設計

## ファイル構成

```
src/app/
├── page.tsx              # ランディングページ
└── (landing)/
    └── components/
        ├── HeroSection.tsx
        ├── FeatureSection.tsx
        ├── WorldSection.tsx
        └── CTASection.tsx
```

## 完了条件

- サービスの魅力が伝わるページになっている
- ログイン導線が明確
- スマホで適切に表示される
