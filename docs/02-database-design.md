# 02. データベース設計（Supabase）

**Status**: TODO
**Priority**: 最優先
**Depends on**: 01-environment-setup

## 概要

Supabaseでのデータベーステーブル設計とRLS（Row Level Security）の設定。

## 関連する要件

- 付録B: データベース設計（REQUIREMENTS.md）

## Tasks

- [ ] usersテーブル作成
  - id, email, google_id, created_at, updated_at
- [ ] booksテーブル作成
  - id, user_id, title, input_type, file_url, ai_summary, created_at
- [ ] questsテーブル作成
  - id, book_id, user_id, world_type, bgm_id, chapter_count, status, created_at
- [ ] chaptersテーブル作成
  - id, quest_id, chapter_number, title, script_text, audio_url, is_free, is_purchased, created_at
- [ ] purchasesテーブル作成
  - id, user_id, quest_id, stripe_payment_id, amount, status, created_at
- [ ] feedbacksテーブル作成
  - id, user_id, quest_id, rating, comment, created_at
- [ ] playback_logsテーブル作成
  - id, user_id, chapter_id, played_at, completed, playback_duration, dropped_at_seconds
- [ ] RLSポリシー設定（各テーブル）
- [ ] TypeScript型定義の生成（supabase gen types）

## テーブル関連図

```
users
  └── books (1:N)
        └── quests (1:N)
              └── chapters (1:N)
              └── feedbacks (1:N)
  └── purchases (1:N)
  └── playback_logs (1:N)
```

## 完了条件

- 全テーブルがSupabaseに作成されている
- RLSが適切に設定されている
- TypeScript型定義が生成されている
