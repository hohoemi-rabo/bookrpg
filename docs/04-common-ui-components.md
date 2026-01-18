# 04. 共通UIコンポーネント

**Status**: TODO
**Priority**: 高
**Depends on**: 01-environment-setup

## 概要

RPG風の世界観を持つ共通UIコンポーネントの作成。

## 関連する要件

- 8. UI/UXデザイン方針（REQUIREMENTS.md）

## Tasks

- [ ] デザイントークンの定義（色、フォント、スペーシング）
- [ ] Buttonコンポーネント（RPG風デザイン）
- [ ] Cardコンポーネント（クエスト表示用）
- [ ] Inputコンポーネント
- [ ] Selectコンポーネント（プルダウン）
- [ ] ProgressBarコンポーネント
- [ ] Modalコンポーネント
- [ ] Loadingコンポーネント（RPG風演出）
- [ ] Headerコンポーネント
- [ ] BottomNavigationコンポーネント（スマホ用）
- [ ] Toastコンポーネント（通知用）

## デザイン方針

- ゲームっぽさを全面に押し出す
- 「学習感」を出さない
- RPGのメニュー画面・クエスト受注画面のような雰囲気

## ファイル構成

```
src/
├── components/
│   └── ui/
│       ├── Button.tsx
│       ├── Card.tsx
│       ├── Input.tsx
│       ├── Select.tsx
│       ├── ProgressBar.tsx
│       ├── Modal.tsx
│       ├── Loading.tsx
│       ├── Header.tsx
│       ├── BottomNav.tsx
│       └── Toast.tsx
└── styles/
    └── tokens.css
```

## 完了条件

- 全コンポーネントが作成されている
- Storybook等でコンポーネントが確認できる（任意）
- レスポンシブ対応（スマホ最優先）
