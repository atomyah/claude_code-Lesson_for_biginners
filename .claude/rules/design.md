# デザインルール

## カラーパレット

| 用途 | Tailwind クラス | 16進数 |
|------|----------------|--------|
| 背景 | `bg-gray-50` | `#f9fafb` |
| カード | `bg-white` | `#ffffff` |
| テキスト（本文） | `text-gray-800` | `#1f2937` |
| テキスト（補助） | `text-gray-500` | `#6b7280` |
| アクセント（ボタン等） | `blue-500` / `blue-600` | `#3b82f6` / `#2563eb` |
| 完了状態 | `text-gray-400` + `line-through` | — |

## タスクカードのスタイル

- 背景: `bg-white`
- 角丸: `rounded-lg`
- 影: `shadow-sm`
- ボーダー: `border border-gray-200`
- パディング: `p-4`

完了状態のカードは `opacity-50` を **インラインスタイル** (`element.style.opacity`) で適用すること（Tailwind 動的クラス禁止のため）。

## タイポグラフィ

- アプリ名: `text-2xl font-bold text-gray-800`
- タスクタイトル: `text-base font-medium text-gray-800`
- メモ: `text-sm text-gray-500`
- 完了タスクのタイトル: 打ち消し線 (`text-decoration: line-through`) をインラインスタイルで適用

## アニメーション

- タスク追加: `transition-opacity duration-300`（`opacity-0` → `opacity-100`）
- タスク削除: `transition-opacity duration-200`（`opacity-100` → `opacity-0`）、アニメーション完了後に DOM から削除

## レスポンシブ

- コンテンツ幅: `max-w-xl mx-auto`（最大 576px、中央寄せ）
- 余白: 横 `px-4`、縦 `py-6`
- タッチデバイスでドラッグハンドルが操作しやすいサイズ（最低 44×44px）を確保すること
