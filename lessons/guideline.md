# 技術スタック学習ガイド

本ドキュメントは、HTML/CSS/JavaScriptの基礎知識を持つ開発者向けに、プロジェクトで使用する技術スタックの学習順序と重要ポイントをまとめたものです。

チーム会議で、随時各技術スタックの解説を行う予定です。

## React基礎

### コンポーネント指向の考え方
- UIをパーツ単位で考える発想
- コンポーネントの再利用性
- プロジェクトでのコンポーネント設計方針

### JSXの基本
- HTMLライクな記法の特徴
- 波括弧{}の使用方法
- コンポーネントの書き方の基本規則

### データの扱い方
- propsによるデータの受け渡し
- stateによる状態管理
- useStateフックの基本的な使い方

### useEffectの適切な使用
- クライアントサイドでの外部APIとの連携（WebSocket等）
- ブラウザAPIの利用（localStorage等）
- サードパーティライブラリの初期化
- イベントリスナーの設定と解除

## モダンReactの新しいパラダイム (推定学習時間: 3-4時間)

### React Server Components (RSC)
- サーバーサイドとクライアントサイドの違い
- "use client" と "use server" ディレクティブ
- RSCのメリット（初期表示の高速化、バンドルサイズの削減）
- RSCでできること・できないこと

### データフェッチの新しいアプローチ
- Server ComponentsでのデータフェッチPベストプラクティス
- React Suspenseを使用したローディング制御
- エラー処理とフォールバックUI

### Client Components
- インタラクティブな機能が必要な場合の使用
- ServerとClientの使い分け
- パフォーマンスの考慮点

## TypeScript入門 (推定学習時間: 2-3時間)

### 型の基本
- 基本的な型定義（string, number, boolean, array）
- オブジェクトの型定義
- 関数の型定義

### Reactでの型定義
- コンポーネントのProps型定義
- イベントハンドラーの型定義
- useState/useEffectでの型指定

## Next.js基礎 (推定学習時間: 2-3時間)

### 基本概念
- App Routerの基本
- ページとレイアウト
- ルーティングの仕組み

### データフェッチング
- Server Componentsでのデータ取得
- Route HandlersでのAPI実装
- キャッシュとrevalidation

## Tailwind CSS & Shadcn/ui (推定学習時間: 2-3時間)

### Tailwind CSSの基本
- ユーティリティファーストの考え方
- よく使用するクラスの説明
- レスポンシブデザインの実装方法

### Shadcn/uiの活用
- 基本的なコンポーネントの使い方
- カスタマイズ方法
- プロジェクトでよく使用するコンポーネント

## Supabase基礎 (推定学習時間: 2-3時間)

### データベースの基本
- テーブル構造の理解
- 基本的なSQLクエリ
- Supabaseクライアントの使用方法

### セキュリティ設定
- RLSの基本概念
- ポリシーの設定方法
- セキュリティ設計の考え方

## Clerk認証 (推定学習時間: 1-2時間)

### 認証の基本
- 認証フローの全体像
- ユーザー情報の取得方法
- 認証状態の管理方法

### アクセス制御
- 保護されたルートの実装
- ロールベースのアクセス制御
- エラーハンドリング

## 実装のベストプラクティス

### データフェッチのパターン
```typescript
// Server Component（推奨）
async function VideoList() {
  const videos = await fetchVideos(); // サーバーサイドで実行
  return <div>{/* 動画一覧の表示 */}</div>;
}

// Client Componentが必要な場合
"use client";
import { useEffect, useState } from "react";

function InteractiveVideo() {
  // クライアントでの状態管理が必要な場合のみuseState/useEffectを使用
  const [isPlaying, setIsPlaying] = useState(false);
  return <div>{/* 再生制御UI */}</div>;
}
```

### レイアウト構成
```typescript
// app/layout.tsx
export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <Header /> {/* 共通ヘッダー */}
        {children}
        <Footer /> {/* 共通フッター */}
      </body>
    </html>
  );
}

// app/videos/layout.tsx
export default function VideosLayout({ children }) {
  return (
    <div>
      <VideosSidebar /> {/* 動画一覧用サイドバー */}
      {children}
    </div>
  );
}
```

## 学習リソース

### 公式ドキュメント
- React: https://react.dev/
- Next.js: https://nextjs.org/docs
- TypeScript: https://www.typescriptlang.org/docs/
- Tailwind CSS: https://tailwindcss.com/docs
- Shadcn/ui: https://ui.shadcn.com/
- Supabase: https://supabase.com/docs
- Clerk: https://clerk.com/docs

### 推奨学習方法
1. まずは各技術の基本概念を理解する
2. 公式ドキュメントのチュートリアルを実施
3. 小さなサンプルプロジェクトで実践
4. プロジェクトのコードを読んで理解を深める

### 注意点
- 完全な理解を目指すのではなく、プロジェクトで必要な部分から優先的に学習する
- 分からないことはチームのSlackで質問する
- 実際のプロジェクトコードを参考にしながら学習を進める
- モダンなアプローチ（RSC等）を優先的に学ぶが、従来の手法も理解しておく


