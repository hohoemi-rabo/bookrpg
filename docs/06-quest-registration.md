# 06. クエスト登録機能（本・テーマ入力）

**Status**: TODO
**Priority**: 高
**Depends on**: 03-authentication, 04-common-ui-components

## 概要

本のタイトル入力またはPDF/画像アップロードによるクエスト登録機能。

## 関連する要件

- 4.2 クエスト登録機能（REQUIREMENTS.md）

## Tasks

### 入力方式A: タイトル入力
- [ ] タイトル入力フォーム作成
- [ ] 注意書き表示「正確なタイトルを入力してください」
- [ ] 入力バリデーション

### 入力方式B: ファイルアップロード
- [ ] ファイルアップロードコンポーネント作成
- [ ] 対応形式チェック（PDF, JPG, PNG）
- [ ] ファイルサイズ制限
- [ ] Cloudflare R2へのアップロード処理
- [ ] アップロード進捗表示

### 入力フロー
- [ ] 入力モード切替UI
- [ ] 追加アップロード機能（内容確認後）
- [ ] 確認画面への遷移

### API
- [ ] POST /api/books（本の登録）

## ファイル構成

```
src/app/
└── (protected)/
    └── quest/
        └── new/
            ├── page.tsx
            └── components/
                ├── TitleInput.tsx
                ├── FileUpload.tsx
                └── InputModeSwitch.tsx
```

## 完了条件

- タイトル入力で本を登録できる
- PDF/画像をアップロードできる
- R2にファイルが保存される
