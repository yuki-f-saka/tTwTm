# tTwTm

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
npm run build
npm run test:e2e # or `npm run test:e2e:ci` for headless testing
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

---

# サンプルコードの構造を理解する

# リアクティブを理解する

# 画面を増やす
- 画面のパスを決める
- router に1つエントリ追加する
- pages に1画面(.vue)追加する

# 画面に動作をつける
- 初期化処理: `<script setup>` を使う
  - 画面内に閉じた state の定義
  - メソッドの定義
- クリックイベント: `<button @click="メソッド名">`
- 変数の中身を画面に描画: `${変数名}`

# 共通store
- pinia使ってる
- state
- actions
- getters
