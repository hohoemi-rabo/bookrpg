---
paths:
  - "src/lib/supabase/**/*"
  - "supabase/**/*"
---

# Database Rules (Supabase)

## Supabase Client

```tsx
// Server Component / Server Action用
import { createServerClient } from '@supabase/ssr'
import { cookies } from 'next/headers'

// Client Component用
import { createBrowserClient } from '@supabase/ssr'
```

## テーブル構成

```
users
  └── books (1:N)
        └── quests (1:N)
              └── chapters (1:N)
              └── feedbacks (1:N)
  └── purchases (1:N)
  └── playback_logs (1:N)
```

## Row Level Security (RLS)

- すべてのテーブルでRLSを有効化
- ユーザーは自分のデータのみアクセス可能

```sql
-- 例: booksテーブルのポリシー
CREATE POLICY "Users can view own books"
ON books FOR SELECT
USING (auth.uid() = user_id);

CREATE POLICY "Users can insert own books"
ON books FOR INSERT
WITH CHECK (auth.uid() = user_id);
```

## データ取得パターン

```tsx
// Server Componentでの取得
const supabase = createServerClient(...)
const { data, error } = await supabase
  .from('books')
  .select('*')
  .order('created_at', { ascending: false })
```

## 認証状態の確認

```tsx
const { data: { user } } = await supabase.auth.getUser()
if (!user) {
  redirect('/login')
}
```

## エラーハンドリング

```tsx
const { data, error } = await supabase.from('books').select()
if (error) {
  console.error('Database error:', error)
  throw new Error('Failed to fetch data')
}
```
