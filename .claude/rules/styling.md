---
paths:
  - "**/*.css"
  - "**/tailwind.config.*"
  - "src/app/**/layout.tsx"
  - "src/components/ui/**/*"
---

# Styling Rules (Tailwind CSS)

## CSS Variables

テーマ用のCSS変数を使用:
- `--background` - 背景色
- `--foreground` - 前景色（テキスト）
- `--font-geist-sans` - サンセリフフォント
- `--font-geist-mono` - モノスペースフォント

## Tailwind設定

Tailwindではこれらの変数を参照:
- `colors.background` → `var(--background)`
- `colors.foreground` → `var(--foreground)`

## ダークモード

`dark:` バリアントでダークモードスタイルを適用:

```tsx
<div className="bg-background text-foreground dark:bg-gray-900 dark:text-white">
  Content
</div>
```

## レスポンシブデザイン

- **スマホファースト**で設計
- ブレークポイント: `sm:`, `md:`, `lg:`, `xl:`

```tsx
<div className="p-4 sm:p-6 md:p-8 lg:p-12">
  {/* モバイル: p-4, タブレット: p-6, デスクトップ: p-8〜 */}
</div>
```

## UIデザイン方針（Book RPG）

- **ゲームっぽさ**を全面に押し出す
- 「学習感」を出さない
- RPGのメニュー画面・クエスト受注画面のような雰囲気
- 操作数は極力少なく

### デザインイメージ

| 画面 | 演出 |
|------|------|
| クエスト登録 | 「依頼を受ける」感覚 |
| 生成中 | 「冒険の準備」演出 |
| 再生 | 「クエスト開始」 |
| ライブラリ | 「冒険の記録」 |

## フォント

- **Geist Sans**: UI、本文
- **Geist Mono**: コード、数値

```tsx
<p className="font-sans">通常のテキスト</p>
<code className="font-mono">コードテキスト</code>
```
