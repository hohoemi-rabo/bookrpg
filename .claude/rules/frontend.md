---
paths:
  - "src/app/**/*.tsx"
  - "src/app/**/*.ts"
  - "src/components/**/*.tsx"
  - "src/components/**/*.ts"
---

# Frontend Rules (Next.js 15 App Router)

## Server Components vs Client Components

- **デフォルトはServer Component** - `'use client'`ディレクティブがない限りServer Componentとして扱われる
- **Client Componentが必要な場合**:
  - `useState`, `useEffect`などのReact Hooksを使用する時
  - ブラウザAPIにアクセスする時（`window`, `localStorage`など）
  - イベントハンドラ（`onClick`, `onChange`など）を使用する時
- **`'use client'`はファイルの先頭に記述** - そのファイルとすべてのインポートがクライアントバンドルに含まれる

```tsx
// Server Component（デフォルト）
export default async function Page() {
  const data = await fetchData()
  return <div>{data}</div>
}

// Client Component
'use client'
export default function Counter() {
  const [count, setCount] = useState(0)
  return <button onClick={() => setCount(count + 1)}>{count}</button>
}
```

## コンポーネント構成パターン

- Server ComponentからClient Componentをインポートして使用する
- Client Componentの`children`としてServer Componentを渡すことで、Server Componentをネストできる

```tsx
// Server Component内でClient Componentを使用
import InteractiveButton from './interactive-button' // Client Component

export default async function Page() {
  const data = await fetchData()
  return (
    <div>
      <h1>{data.title}</h1>
      <InteractiveButton />
    </div>
  )
}
```

## Loading & Error Handling

- `loading.tsx` - Suspenseフォールバック（ローディングUI）
- `error.tsx` - エラーバウンダリ（**必ず`'use client'`が必要**）
- `not-found.tsx` - 404ページ

```tsx
// error.tsx
'use client'

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    <div>
      <h2>エラーが発生しました</h2>
      <button onClick={() => reset()}>再試行</button>
    </div>
  )
}
```

## Suspenseの活用

- 動的データを取得するコンポーネントを`<Suspense>`でラップ
- `headers()`, `cookies()`へのアクセスはSuspense境界内で行う

```tsx
import { Suspense } from 'react'

export default function Page() {
  return (
    <Suspense fallback={<Loading />}>
      <AsyncComponent />
    </Suspense>
  )
}
```

## Metadata（SEO）

- 静的メタデータ: `metadata`オブジェクトをエクスポート
- 動的メタデータ: `generateMetadata`関数を使用
- レイアウトで`title.template`を設定すると子ページのタイトルに適用される

```tsx
// 静的メタデータ
export const metadata: Metadata = {
  title: 'ページタイトル',
  description: '説明文',
}

// 動的メタデータ
export async function generateMetadata({ params }: Props): Promise<Metadata> {
  const { id } = await params
  const product = await getProduct(id)
  return { title: product.name }
}

// レイアウトでテンプレート設定
export const metadata: Metadata = {
  title: {
    template: '%s | BookRPG',
    default: 'BookRPG',
  },
}
```

## Dynamic Routes

- `[slug]` - 動的セグメント
- `[...slug]` - Catch-all セグメント
- `[[...slug]]` - Optional catch-all セグメント
- Next.js 15では`params`はPromiseとして渡される

```tsx
// app/posts/[slug]/page.tsx
export default async function Page({
  params,
}: {
  params: Promise<{ slug: string }>
}) {
  const { slug } = await params
  const post = await getPost(slug)
  return <article>{post.content}</article>
}
```
