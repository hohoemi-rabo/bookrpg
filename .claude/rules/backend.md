---
paths:
  - "src/app/api/**/*.ts"
  - "src/lib/**/*.ts"
  - "src/actions/**/*.ts"
---

# Backend Rules (API Routes & Server Actions)

## Data Fetching

- **Server Componentで直接`fetch`を使用**
- **キャッシュ戦略**:
  - `cache: 'force-cache'`（デフォルト）- 静的データ、手動で無効化するまでキャッシュ
  - `cache: 'no-store'` - 毎リクエストで再取得（動的データ）
  - `next: { revalidate: 秒数 }` - 指定秒数後に再検証

```tsx
// 静的データ（キャッシュされる）
const staticData = await fetch('https://...', { cache: 'force-cache' })

// 動的データ（毎回取得）
const dynamicData = await fetch('https://...', { cache: 'no-store' })

// 10秒ごとに再検証
const revalidatedData = await fetch('https://...', { next: { revalidate: 10 } })
```

## Server Actions

- フォーム送信やデータ変更には**Server Actions**を使用
- `'use server'`ディレクティブで定義
- `revalidatePath`または`revalidateTag`でキャッシュを無効化

```tsx
// actions.ts
'use server'

import { revalidatePath } from 'next/cache'
import { redirect } from 'next/navigation'

export async function createPost(formData: FormData) {
  const title = formData.get('title')
  // データベース操作
  await db.posts.create({ title })

  revalidatePath('/posts')  // キャッシュを無効化
  redirect('/posts')        // リダイレクト
}
```

```tsx
// page.tsx
import { createPost } from './actions'

export default function Page() {
  return (
    <form action={createPost}>
      <input name="title" />
      <button type="submit">Create</button>
    </form>
  )
}
```

## Route Handlers（API Routes）

- `app/api/*/route.ts`でHTTPエンドポイントを定義
- GET, POST, PUT, DELETE等のHTTPメソッドをエクスポート

```tsx
// app/api/posts/route.ts
import { NextResponse } from 'next/server'

export async function GET() {
  const posts = await getPosts()
  return NextResponse.json(posts)
}

export async function POST(request: Request) {
  const data = await request.json()
  const post = await createPost(data)
  return NextResponse.json(post, { status: 201 })
}
```

## エラーハンドリング

- API Routesでは適切なHTTPステータスコードを返す
- try-catchでエラーをキャッチし、ログを残す

```tsx
export async function POST(request: Request) {
  try {
    const data = await request.json()
    const result = await processData(data)
    return NextResponse.json(result, { status: 201 })
  } catch (error) {
    console.error('API Error:', error)
    return NextResponse.json(
      { error: 'Internal Server Error' },
      { status: 500 }
    )
  }
}
```

## Webhook処理

- 署名検証を必ず行う
- 冪等性を考慮した設計にする

```tsx
// Stripe Webhook example
export async function POST(request: Request) {
  const body = await request.text()
  const signature = request.headers.get('stripe-signature')!

  const event = stripe.webhooks.constructEvent(
    body,
    signature,
    process.env.STRIPE_WEBHOOK_SECRET!
  )

  // イベント処理
}
```
