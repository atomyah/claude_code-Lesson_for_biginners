# Tailwind CSS ルール

## 動的クラス禁止

TailwindCSS Play CDN は、JS の実行時に生成されるクラス名を検出できない。
以下のような書き方は**禁止**。

```js
// NG: Play CDN がクラスを認識しない
element.className = `bg-${color}-500`;
element.classList.add(`opacity-${value}`);
const cls = completed ? 'opacity-50' : 'opacity-100';
element.className = cls; // 条件式でも検出不可の場合がある
```

動的なスタイルは必ずインラインスタイルで適用すること。

```js
// OK: インラインスタイルを使う
element.style.opacity = completed ? '0.5' : '1';
element.style.textDecoration = completed ? 'line-through' : 'none';
element.style.color = completed ? '#9ca3af' : '#1f2937';
```

## 静的クラスは問題なし

HTML に直書きするクラス名、または JS で固定文字列として渡すクラスは問題なし。

```js
// OK: 固定文字列
element.classList.add('hidden');
element.classList.remove('hidden');
element.classList.add('opacity-50'); // 固定値なら可（ただし動的生成はNG）
```

## CDN バージョン

```html
<script src="https://cdn.tailwindcss.com"></script>
```

`tailwind.config` のカスタマイズが必要な場合は CDN スクリプト直後に追加する。
