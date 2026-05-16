# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

**ToDo リスト Web アプリ** — ローカル専用。ブレイン・ラボ ClaudeCodeレッスンの一環として開発。デプロイなし、ビルドツールなし。

詳細な機能仕様は `spec.md` を参照。

## 技術スタック

- HTML + TailwindCSS Play CDN (ビルド不要)
- Vanilla JS (IIFE パターン)
- SortableJS v1.15.6 (CDN) — ドラッグ&ドロップ
- LocalStorage (`todo-tasks` キー) — データ永続化

## 開発方法

ビルドステップなし。`index.html` をブラウザで直接開くだけで動作する。

```
# ブラウザで開く（Windows）
start index.html
```

## ファイル構成

```
project_root/
├── CLAUDE.md              # 本ファイル（Claude Code 向け指示）
├── spec.md                # 機能仕様書
├── index.html             # アプリ本体（HTML + CSS + JS を単一ファイルに集約）
└── .claude/
    └── rules/
        ├── design.md      # デザインルール（カラー・レイアウト・アニメーション）
        ├── tailwind.md    # Tailwind 制約（動的クラス禁止など）
        └── javascript.md  # JS コーディング規約（命名・関数設計・XSS対策）
```

## アーキテクチャ

全コードを `index.html` 1 ファイルに収める構成。JS は IIFE (`(function() { ... })()`) で囲み、グローバルスコープ汚染を防ぐ。

**データフロー:** UI イベント → JS 関数 → LocalStorage 読み書き → DOM 更新

## 重要な制約と規約

詳細は各ルールファイルを参照すること。

### @.claude/rules/tailwind.md
### @.claude/rules/javascript.md
### @.claude/rules/design.md
