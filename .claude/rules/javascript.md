# JavaScript コーディング規約

## 基本方針

- Vanilla JS のみ使用（フレームワーク・ライブラリは SortableJS のみ許可）
- 全スクリプトを IIFE で囲みグローバルスコープ汚染を防ぐ

```js
(function () {
  'use strict';
  // すべてのコードをここに記述
})();
```

## データ管理

- LocalStorage キー: `todo-tasks`
- 読み書きは専用関数（`loadTasks` / `saveTasks`）を通じて行う
- ID は `Date.now().toString(36) + Math.random().toString(36).slice(2)` で生成

```js
function loadTasks() {
  try {
    return JSON.parse(localStorage.getItem('todo-tasks') || '[]');
  } catch {
    return [];
  }
}

function saveTasks(tasks) {
  localStorage.setItem('todo-tasks', JSON.stringify(tasks));
}
```

## DOM 操作

- `innerHTML` を使う場合はユーザー入力を必ずエスケープする（XSS 対策）

```js
function escapeHtml(str) {
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
}
```

- `textContent` を使えば自動でエスケープされるので積極的に活用する

## 命名規則

| 種別 | 規則 | 例 |
|------|------|----|
| 変数・関数 | camelCase | `taskList`, `addTask()` |
| 定数 | UPPER_SNAKE_CASE | `STORAGE_KEY` |
| DOM 要素変数 | `el` プレフィックス + PascalCase | `elTaskList`, `elAddBtn` |

## 関数設計

- 1 関数 1 責務を維持する
- 副作用（DOM 更新・LocalStorage 書き込み）は呼び出し側で明示的に行う
- 純粋関数（入力 → 出力のみ）と副作用関数を分離する

```js
// 純粋関数（データ操作）
function toggleTask(tasks, id) {
  return tasks.map(t => t.id === id ? { ...t, completed: !t.completed } : t);
}

// 副作用関数（DOM + LocalStorage）
function handleToggle(id) {
  tasks = toggleTask(tasks, id);
  saveTasks(tasks);
  renderTasks();
}
```

## エラーハンドリング

- LocalStorage の読み書きは `try/catch` で囲む
- ユーザーに影響するエラーはコンソールではなく UI に表示する（入力バリデーション等）
