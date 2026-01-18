# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## ルールファイルについて

詳細なルールは `.claude/rules/` 配下に分割管理しています：

| ファイル | 適用対象 |
|----------|----------|
| `frontend.md` | `src/app/**/*`, `src/components/**/*` |
| `backend.md` | `src/app/api/**/*`, `src/lib/**/*`, `src/actions/**/*` |
| `styling.md` | `**/*.css`, `**/tailwind*` |
| `database.md` | Supabase関連の作業時 |
| `ai-integration.md` | `src/lib/gemini/**/*` |

**ユーザーへ**: 「CLAUDE.md更新して」と言えば、内容に応じて適切なファイルに振り分けます。

## チケット管理ルール

- チケットファイルは `/docs/` 配下に連番で管理
- 各チケット内のTodoは以下の形式で管理:
  - `- [ ]` 未完了タスク
  - `- [x]` 完了タスク
- タスク完了時は `- [ ]` を `- [x]` に変更すること
- チケットのステータス管理:
  - `Status: TODO` - 未着手
  - `Status: IN_PROGRESS` - 作業中
  - `Status: DONE` - 完了

## Development Commands

```bash
npm run dev      # Start development server with Turbopack (http://localhost:3000)
npm run build    # Production build with Turbopack
npm run start    # Start production server
npm run lint     # Run ESLint
```

## Tech Stack

- **Framework**: Next.js 15.5 with App Router
- **Language**: TypeScript (strict mode)
- **Styling**: Tailwind CSS 3.4
- **Fonts**: Geist Sans / Geist Mono (via next/font)
- **Backend**: Supabase
- **AI**: Gemini 2.5
- **Storage**: Cloudflare R2
- **Payment**: Stripe

## Project Structure

```
src/
├── app/           # App Router pages and layouts
├── components/    # 共通UIコンポーネント
├── lib/           # ユーティリティ、外部サービス連携
├── actions/       # Server Actions
└── types/         # TypeScript型定義
```

- `@/*` path alias maps to `./src/*`

## ESLint Configuration

Uses flat config (`eslint.config.mjs`) with:
- `next/core-web-vitals`
- `next/typescript`
